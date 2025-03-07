
# 5.2 Resource Management 

A resource is something that must be aquired and later be released, these are things such as memory, locks, sockets, thread handles, and file handles.

Failing to release a resource in a timely manner is known as a "leak" and can causes performance degradation

Example of Standard Library lock classes:
```c++
mutex m; // used to protect access to shared data
// ...
void f()
{
	unique_lock<mutex> lck {m}; // acquire the mutex m
	// ... manipulate shared data ...
}
```

So a `thread` will not proceed until `lck`s constructor has acquired its `mutex`, `m`

In this example `unique_lock`s deconstructor releases the `mutex` when the thread of control leaves  `f()`

This is an application of "Resource Acquisition Is Initialized"

## 5.2.1 `unique-ptr` and `shared_ptr`

In `<memory>` the standard library provides 2 smart pointers to help manage objects on the free store:
1. `unique_ptr` to represent unique ownership
2. `shared_ptr` to represent shared ownership

The most basic use of smart pointers is to prevent memeory leaks caused by careless programming for example:
```c++
void f(int i, int j)
 // X* vs. unique_ptr<X>
{
	X∗ p = new X;// allocate a new X
	unique_ptr<X> sp {new X}; // allocate a new X and give its pointer to unique_ptr
	if (i<99) throw Z{}; // may throw an exception
	if (j<77) return; // may return "early"
	p−>do_something(); // may throw an exception
	sp−>do_something(); // may throw an exception
	// ...
	delete p; // destroy *p

```

So in this example we forgot to delete `p` if i<99 or if j<77. On the other hand `unique_ptr` ensures that its object is properly destroyed whichever way we exit the function `f()`

`unique_ptr` is very lightweight mechanism with no space or item overhead compared to the built-in pointer. 
We can also include passing free-store allocated objects in and out of functions: 
```c++
unique_ptr<X> make_X(int i)
// make an X and immediately give it to a unique_ptr
{
	// ... check i, etc. ...
	return unique_ptr<X>{new X{i}};
}
```

The `unique_ptr` is a handle to an individual object in the same way that `vector` is a handle to a sequence of objects; in which both control the lifetime of other object. 

The `shared_ptr` is similar to that of the `unique_ptr` except that `shared_ptr`s are copied rather than moved.

The `shared_ptr`s for an object share ownership of an object and that object is destroyed when the last of its `shared_ptr`s is destroyed for example:
```c++
void f(shared_ptr<fstream>);
void g(shared_ptr<fstream>);
void user(const string& name, ios_base::openmode mode)
{
	shared_ptr<fstream> fp {new fstream(name ,mode)};
	if (!∗fp) throw No_file{}; // make sure the file opened
	f(fp);
	g(fp);
	// ...
}
```

Now, the file opened by `fp`’s constructor will be closed by the last function to (explicitly or implicitly) destroy a copy of `fp`. Note that `f()` or `g()` may spawn a task holding a copy of `fp` or in some other way store a copy that outlives `user()`. 

# 5.3 Concurrency

**Concurrency**: the execution of several tasks simultaneously

## 5.3.1 Tasks and `thread`s

**Task**: a task is a computation that can potentially be executed concurrently with other computations
**Thread**: the system-level representation of a task ina program

So a task can be executed concurrently with other tasks is launched by constructing a `std::thread` in the `<thread>` library with a task as its argument. 

For example:
```c++
void f();  // function

struct F { // function object
void operator()();// F’s call operator (§3.4.3)
};


void user()
{
thread t1 {f}; // f() executes in separate thread
thread t2 {F()}; // F()() executes in separate thread

t1.join(); // wait for t1
t2.join(); // wait for t2

}
```

The `join()` ensures that we dont exit `user()` until the threads have completed so to join means to wait for the thread to terminate

Threads of a program share a single address space which means they can communicate through shared objects. Such communication is typically controlled by locks or other mechanisms to prevent data races. 

When defining tasks of a concurrent program, our aim is to keep tasks completely separate except where they communicate in simple and obvious ways.

For that to work, we just have to pass arguments, get a result back, and make sure that there is no use of shared data in between (no data races).

## 5.3.2 Passing Arguments

Consider the example:
```c++
void f(vector<double>& v);// function do something with v

struct F { // function object: do something with v
	vector<double>& v;
	F(vector<double>& vv) :v{vv} { }
	void operator()();  // application operator; §3.4.3
};

int main()
{
	vector<double> some_vec {1,2,3,4,5,6,7,8,9};
	vector<double> vec2 {10,11,12,13,14};
	thread t1 {f,some_vec}; // f(some_vec) executes in a separate thread
	thread t2 {F{vec2}};// F(vec2)() executes in a separate thread
	
	t1.join();
	t2.join();
}

```

Here `F{vec2}` saves a reference to the argument vector in `F`. So `F` can now use that array and hopefully no other task access `vec2` while `F` is executing. Passing `vec2` by value would eliminate that risk

## 5.3.4 Sharing Data

Sometimes tasks need to share data. In that case the access has to be synchronized so that at most one task at a time has access to the data. 

The fundamental element for this is the `mutex` a "mutual exclusion object"
. Where a `thread` will acquire a mutex using a `lock()` operation for example:
```c++
mutex m; // controlling mutex
int sh; // shared data

void f()
{
	unique_lock<mutex> lck {m}; // acquire mutex
	sh += 7; // manipulate shared data
} // release mutex implicitly
```

The `unique_lock`’s constructor acquires the mutex (through a call `m.lock()`). If another thread has already acquired the mutex, the thread waits (‘‘blocks’’) until the other thread completes its access.

Once a thread has completed its access to the shared data, the `unique_lock` releases the mutex (with a call `m.unlock()`). 

**Dead lock**: when the waiting process is still holding on to another resource that the first needs before it can finish.

For example, if `thread1` acquires `mutex1` and then tries to acquire `mutex2` while `thread2` acquires `mutex2` and then tries to acquire `mutex1`, then neither task will ever proceed further.

One way around this is :
```c++
void f()
{
	// ...
	unique_lock<mutex> lck1 {m1,defer_lock}; // defer_lock: don’t yet try to acquire the mutex
	unique_lock<mutex> lck2 {m2,defer_lock};
	unique_lock<mutex> lck3 {m3,defer_lock};
	// ...
	lock(lck1,lck2,lck3); // acquire all three locks
	// ... manipulate shared data ...
} // implicitly release all mutexes
```

This `lock()` will only proceed after acquiring all its `mutex` arguments and will never block (‘‘go to sleep’’) while holding a `mutex`. The destructors for the individual `unique_locks` ensure that the `mutexe`s are released when a `thread` leaves the scope.

### 5.3.4.1 Waiting for Events

Sometimes a `thread` needs to wait for some kind of external event before proceeding

The basic support for communicating using external events is provided by `condition_variable`s found in `<condition_variable>`

A `condition_variable` is a mechanism allowing one thread to wait for some condition (often refereed to as an event) to occur as the result of work done by other `thread`s

Consider an example where 2 `thread`s are communicating by passing messages through a `queue`
```c++
class Message { // object to be communicated
// ...
};
queue<Message> mqueue; // the queue of messages
condition_variable mcond; // the variable communicating events
mutex mmutex;// the locking mechanism
```
The `consumer() `reads and processes `Message`s:
```c++
void consumer()
{
	while(true) {
		unique_lock<mutex> lck{mmutex}; // acquire mmutex
		while (mcond.wait(lck)) /* do nothing */;
		auto m = mqueue.front(); // get the message
		mqueue.pop();
		lck.unlock(); // release lck
		// ... process m ...
	}
}
```
The corresponding `producer` looks like this:
```c++
void producer()
{
	while(true) {
		Message m;
		// ... fill the message ...
		unique_lock<mutex> lck {mmutex}; // protect operations
		mqueue.push(m);
		mcond.notify_one(); // notify
	} // release lock (at end of scope)
}
```

## 5.3.5 Communicating Tasks

`future` and `promise` for returning a value from a task spawned on a separate thread
`packaged_task` to help launch tasks and connect up the mechanisms for returning a result
`async()` for launching of a task in a manner very similar to calling a function.

These are found in the `<future>` library 

### 5.3.5.1 `future` and `promise`

The biggest use of the `future` and `promise` is that they allow transfer of a value between 2 tasks without explicit use of a lock 

So when a task wants to pass a value to another it puts the value `promise`. Then the implementation makes that value appear in the corresponding `future`

![[PromiseFuture.png]]


Assume we have a `future<X>` called `fx` we can `get()` a value of type `X` from it by:
```c++
X v = fx.get(); 
```

The main purpose of a promise is to `provide` simple ‘‘put’’ operations (called `set_value()` and `set_exception()`) to match future’s `get()`.

If we need to have a `promise` pass a result of type `X` to a `future` we can do this in 2 ways: pass a value or pass an exception:

```c++
void f(promise<X>& px){ // a task: place the result in px
	//...
	try{
		X res;
		//copmute a value for res
		px.set_value(res)
	}
	catch(...){ //couldnt compute res
		//pass the exeption to the future thread
		px.set_exception(current_exception());
	}
}
```

To deal with the exception transmitted through the a `future` the caller of `get()` must be prepared to catch it somewhere for example:
```c++
void g(future<X>& fx){
	// ..
	try{
		X v = fx.get(); //if necessary wait for the value
		// use v
	}
	catch(...){ // oops: cant copmute v 
		//handle error
	}
}
```

### 5.3.5..2 `packaged_task`

So how do we get a `future` into a task that needs a result and the corresponding `promise` into a thread that should produce that result

The `packaged_task` provides a way of connecting `future`s and `promise`s to be run on `thread`s

A packaged_task provides wrapper
code to put the return value or exception from the task into a promise (like the code shown in
§5.3.5.1). If you ask it by calling get_future, a packaged_task will give you the future corresponding
to its promise.

For example:
```c++
double accum(double∗ beg, double ∗ end, double init)
// compute the sum of [beg:end) starting with the initial value init
	{
	return accumulate(beg,end,init);
	}
	
double comp2(vector<double>& v)
{
	using Task_type = double(double∗,double∗,double);// type of task
	
	packaged_task<Task_type> pt0 {accum}; // package the task (i.e., accum)
	packaged_task<Task_type> pt1 {accum};
	
	future<double> f0 {pt0.get_future()}; // get hold of pt0’s future
	future<double> f1 {pt1.get_future()}; // get hold of pt1’s future
	
	
	double∗ first = &v[0];
	thread t1 {move(pt0),first,first+v.size()/2,0}; // start a thread for pt0
	thread t2 {move(pt1),first+v.size()/2,first+v.siz e(),0};// start a thread for pt1
	
	// ...
	return f0.get()+f1.get();
}

```

### 5.3.5.3 `async()`

To launch tasks to potentially run asynchronously, we can use `async()`:

```c++
double comp4(vector<double>& v)
// spawn many tasks if v is large enough
{
	if (v.siz e()<10000) return accum(v.begin(),v.end(),0.0);
	auto v0 = &v[0];
	auto sz = v.size();
	auto f0 = async(accum,v0,v0+sz/4,0.0); // first quarter
	auto f1 = async(accum,v0+sz/4,v0+sz/2,0.0); // second quarter
	auto f2 = async(accum,v0+sz/2,v0+sz∗3/4,0.0); // third quarter
	auto f3 = async(accum,v0+sz∗3/4,v0+sz,0.0); // fourth quarter
	
	return f0.get()+f1.get()+f2.get()+f3.get(); // collect and combine the results
}
```

So basically `async()` separates the call part of a function from the get the result part and separates both from the actual execution of the task. So using `async()` we dont have to think about threads and locks

Though it is not really possible to use `async()` for tasks that share resources needing locking, as we dont know how many `thread`s will be used as `async()` decides that based on what it knows fo the system resources available at the time of the call. 