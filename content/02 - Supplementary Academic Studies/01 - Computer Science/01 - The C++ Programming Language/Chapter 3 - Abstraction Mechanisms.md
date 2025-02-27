# 3.2 Classes

A **class** is a user-defined type provided to represent a concept in the code of a program
Commonly classes fall into 3 disctint kinds:
1. Concrete Classes
2. Abstract Classes
3. Classes in class Hierarchies
## 3.2.1 Concrete Types

The basic idea of **concrete classes** is that they behave just like built in types

For example a class like complex number type is similar to a built in type like int though they have their own set of operations and semantics. 

### 3.2.1.1 An Arithmetic Type

The classical user-defined arithmetic type is `complex` which can be defined as 
```c++
class complex {
double re, im; // representation: two doubles
public:
	complex(double r, double i) :re{r}, im{i} {} // construct complex from two scalars
	complex(double r) :re{r}, im{0} {} // construct complex from one scalar
	complex() :re{0}, im{0} {} // default complex: {0,0}

	double real() const { return re; }
	void real(double d) { re=d; }
	double imag() const { return im; }
	void imag(double d) { im=d; }
	
	complex& operator+=(complex z) { re+=z.re, im+=z.im; return ∗this; }
	
	complex& operator−=(complex z) { re−=z.re, im−=z.im; return ∗this; }
	
	complex&operator∗=(complex);
	complex&operator/=(complex);
};

```
A constructor that can be invoked without an argument is called a **default constructor**. Above this is the line `complex() :re{0}, im{0} {}`

### 3.2.1.2 A Container

A **container** is an object that holds a collection of elements such as `vector`

*Resource Acquisition Is Initialization* or *RAII*, allows us to eliminate ‘‘naked new operations,’’ that is, to avoid allocations in general code and keep them buried inside the implementation of well-behaved abstractions.

## 3.2.2 Abstract Types

**Abstract Type** is a type that completely insulates a user from implementation details. 

Since we don’t know anything about the representation of an abstract type (not even its size), we must allocate objects on the free store and access them through references or pointers.

For example we can have a container:
```c++
class container{
public:
	virtual double& operator[](int) = 0; 
	virtual int size() const = 0;
	virtual ~Container() {}
};
```

Here the `virtual` means may be redefined later in a class derived from this one

The syntax `=0` says that the function is **pure virtual** that is some class derived from `container` must define the function

Thus it is not possible to define an object that is just a `container`; rather a `container` serves as the interface to a class that implements its `operator[]()` and `size()` functions. 

Using the Vector example we can implement the functions required by container as:
```c++
class Vector_container: public Container{
	Vector v;
public:
	Vector_container(int s): v(s) {}
	~Vector_container(){}

	double& operator[](int i) {return v[i];}
	int size() const{return v.size();}
};
```

Here the `:public` can be read as is derived from or is a subtype of. 

Class `Vector_container` is said to be **derived** from class `Container` and class `Container` is said to be a **base** of class `Vector_container`

An alternative to this naming convention would be `Vector_container` and `Container` being the **subclass** and **superclass** respectively 

The derived class is said to inherit members from its base class so the use of base and derived classes is commonly referred to as **inheritance**

The members `operator[]()` and `size()` are said to **override** the corresponding members in the base class `container`

## 3.2.3 Virtual Functions

The usual implementation technique is for the compiler to convert the name of a virtual function into an index into a table of pointers to functions
This is called the *virtual function table* or the `vtbl`, and each class with virtual functions has its own `vtbl` identifying its virtual functions

## 3.2.4 Class Hierarchies

*Interface Inheritance*: An object of a derived class can be used wherever an object of a base class is required. 
*Implementation Inheritance*: A base class provides functions or data that simplifies the implementation of derived functions. Ex: `simely` use of `Circles` constructor and `Circle::draw()` method

`unique_ptr`: will delete itself when the object goes out of scope
```c++
unique_ptr<Shape> read_shape(istream& is) // read shape descriptions from input stream is
{
	switch (k) {
		case Kind::circle:
		// read circle data {Point,int} into p and r
		return unique_ptr<Shape>{new Circle{p,r}};
	// ...
}

// §5.2.1
void user()
{
	vector<unique_ptr<Shape>> v;
	while (cin)
		v.push_back(read_shape(cin));
	draw_all(v);
	 // call draw() for each element
	rotate_all(v,45); // call rotate(45) for each element
} // all Shapes implicitly destroyed
```

# 3.3 Copy and Move

## 3.3.1 Copying Containers

Copying of an object of a class is defined by two members, *copy constructor* and a *copy assignment*
```c++
class Vector {
private:
	double∗ elem; // elem points to an array of sz doubles
	int sz;
public:
	Vector(int s); // constructor: establish invariant, acquire resources
	Vector() { delete[] elem; } // destructor: release resources
	
	Vector(const Vector& a);// copy constructor
	Vector& operator=(const Vector& a);// copy assignment

	double& operator[](int i);
	const double& operator[](int i) const;
	int size() const;
};
```

## 3.3.2 Moving Containers

Moving containers in C++ typically involves transferring ownership of the contents from one container to another without performing expensive deep copies

```c++
class Vector {
// ...
	Vector(const Vector& a);// copy constructor
	Vector& operator=(const Vector& a);// copy assignment

	Vector(Vector&& a);// move constructor
	Vector& operator=(Vector&& a); // move assignment

};


```

The `&&` means "rvalue refernce" and is a reference to which we can bind an rvalue. Really a rvalue is a value that you cant assign to and an rvalue reference is a reference to something that nobody else can assign to. 

So really after a move the original object has no specified state and the object with the moved items has the ownership now. 

## 3.3.3 Resource Management
?

## 3.3.4 Suppressing Operations
?

# 3.4 Templates

A *template* is a class or a function that we parameterize with a set of types or values. 

## 3.4.1 Parameterized Types

We can generalize a class of a specific type to a class of any type by making it a template and replacign specific types, for example:
```c++
template<typename T>
class Vector {
private:
	T∗ elem; // elem points to an array of sz elements of type T
	int sz;
public:
	Vector(int s); // constructor: establish invariant, acquire resources
	~Vector() { delete[] elem; }// destructor: release resources
	// ... copy and move operations ...
	T& operator[](int i);
	const T& operator[](int i) const;
	int size() const { return sz; }
};

```
- pg 78 after example