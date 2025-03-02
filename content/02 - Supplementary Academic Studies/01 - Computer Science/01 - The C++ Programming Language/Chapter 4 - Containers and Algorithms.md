
- Skipped the really introductory libraries 
![[Pasted image 20250227162638.png]]![[Pasted image 20250227162647.png]]

## 4.3.3 I/O of User-Defined Types

The `iostream` library allows programmers to define I/O for their own types.  For example lets create a type `Entry` like ;
```c++
 struct Entry{
	string name;
	int number;
}
```

we can then define a simple output operator to write an `Entry` :
```c++
ostream& operator<<(ostream& os, const Entry& e){
	return os<<"{\"<<e.name<<"\"," << e.number<<"}";
	}
```

We can also define a read in for `Entry` as:
```c++
istream& operator>>(istream& is, Entry& e)
// read { "name" , number } pair. Note: for matted with { " " , and }
{
	char c, c2;
	if (is>>c && c=='{' && is>>c2 && c2=='"') { // start with a { "
	string name; // the default value of a string is the empty string: ""
	while (is.get(c) && c!='"') // anything before a " is part of the name
		name+=c;

	if (is>>c && c==',') {
		int number = 0;
		if (is>>number>>c && c=='}') { // read the number and a }
			e = {name,number};// assign to the entry
			return is;
		}
	}
}
	is.setf(ios_base::failbit); // register the failure in the stream
	return is;
}

```

# 4.4 Containers

**Container**: a class with the main purpose of holding objects

## 4.4.1 `vector`

A **vector** is a sequence of elements of a given type, and these elements are stored contiguously in memory. 

When we define a `vector` we give it an initial size:
```c++
vector<int> v1 = {1,2,3,4}; //size is 4
vector<string> v2; //size is 0
vector<Shape *> v3(23); //size is 23; and inital element values: nullptr
vector<double> v(32,9.9); //size is 32; inital element value 9.9
```

Here the second entry to the vector would specify the default value, so for the last example all 32 elements would have the initial value of 9.9 .

### 4.4.1.1 Elements

`vector` is a container of elements of some type `T` that is to say `vector<T>`. Just about any type qualifies as an element type:
- built in numeric types (`int,double` etc)
- user-defined types (`Entry,Matrix` etc)
- pointers (`const char*, Shape*` etc)

The standard `vector` library does not guarantee range checking so an element that is not there can still be accessed.

## 4.4.2 `list`

`list` is equivalent to a doubly linked list

Example:
```c++
list<Entry> phone_book = {
	{"David Hume",123456},
	{"Karl Popper",234567},
	{"Bertrand Ar thur William Russell",345678}
};
```
```c++
int get_number(const string& s)
{
	for (const auto& x : phone_book)
		if (x.name==s)
			return x.number;
	return 0; // use 0 to represent "number not found"
}
```

Adding elements and removing elements to a list is easy:
```c++
void f(const Entry& ee, list<Entry>::iterator p, list<Entry>::iterator q)
{
	phone_book.insert(p,ee); // add ee before the element referred to by p
	phone_book.erase(q); // remove the element referred to by q
}
```

## 4.4.3 `map`

A `map` is essentially a associative array or a dictionary, and its implementation is a balanced binary tree. 
A `map` is a container of pairs of key, values for example:
```c++
map<string,int> phone_book {
	{"David Hume",123456},
	{"Karl Popper",234567},
	{"Bertrand Ar thur William Russell",345678}
};
```

We can index by a value of its first type (`key`) and the `map` will return with the corresponding value of the second type `value` for example:
```c++
int get_number(const string& s)
{
	return phone_book[s];
}
```

And if a key isn't found it is entered into the map with a default value for its value, so to avoid this functionality we can use the `find()` and `insert()` instead of `[]`

The cost to lookup in a `map` is $O(log(n))$ where `n` is the number of elements in the map
## 4.4.4 `unordered_map`

`unordered_map` is similar to a `map` though it uses a hashed lookup rather than comparison.

For example the phone book example would look like: 
```c++
unordered_map<string,int> phone_book {
	{"David Hume",123456},
	{"Karl Popper",234567},
	{"Bertrand Ar thur William Russell",345678}
};
```
## 4.4.5 Container Overview

![[Container Overview.png]]


# 4.5 Algorithms

- Put a pin here kinda general knowledge but could be good to go back over- it goes into deeper detail in chapter 32 so might look back there 