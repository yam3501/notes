# What is Ownership?
_Ownership_ is a set of rules that govern how a Rust program manages memory.

Memory is managed through a system of ownership with a set of rules that compiler checks. If any of the rules are validated, program won't compile.

None of the features of ownership slow down the program.

---------------

## The _Stack_ and the _Heap_:

BOth stack and heap are part of memory available to the code to use at runtime.

_Stack_ stores values in the order it gets them and removes the values in opposite order. This is referred to as LIFO.

Adding data is called _pushing onto the stack_, removing data is called _popping off the stack_.

All data stored on the stack must have a known, fixed size.

_Heap_ is less organized. When you put data onto the heap, you request certain amount of space. The memory allocator finds an empty spot in the heap, marks it as being in use and returns a pointer which is the address of that location. This process is called_allocating on the heap_.

-----------

Pushing values onto the stack is not considered allocating.

-----------

Because the pointer to the heap is known, fixed size, you can store the value on the stack, but when you want the actual data, you must follow the pointer.

Pushing onto the stack is faster than allocating on the heap because the allocator never has to search for a place to store new data; that location is always on top of the stack.

----------

Allocating space on the heap reequires more work because the allocator must first find a big enough space to hold the data and then perform bookkepping to prepare for the next allocation.

Accessing data on the heap is slower than accessing data on the stack because you have to follow a pointer to get there. Contemporary preocessors are faster if they jump around less in memory. A processor can do its job better on data that's close to other data - as it is on the stack; rather than farther away - as it is on the heap.

When your code calls a function, the values passed into the function (including potentially pointers to data on the heap) and the functions local variables get pushed onto the stack. When the function is over, the values are popped off.

Keeping track of what parts of code are using what data on the heap, minimizing amount of duplicate data on the heap and cleaning up unused data are all problems ownership addresses.

Main purpose of ownership is to address heap data.

--------------

## Ownership Rules:

1] Each value in Rust has an "owner"
2] There can only be one owner at a time.
3] When the owner goes out of scope, the value is dropped.

-----------------

## Variable Scope:

Eg.

'''

//s is invalid

let s = "hello"; //s is valid

// do stuff with s

} // scope is over so s is invalid

'''

* When s comes _into_ scope, it is valid.
* It remains valid until it goes _out_ of scope.

--------------------------

## The String Type:

To illustrate rules of ownership, we need a data typoe which is more complex than those covered before. String types is a great example.

String literals are convenient, but aren't suitable for every situation in which we may want to use test. One reason is they're immutable and another is that not every string value can be known when we write our code.

In such cases Rust has second string type, _String_.This type manages data allocated on the heap and is able to store an amount of text that is unknown to us at compile time. You can create a String from a string literal using the _from_ function: 

'''

let s = String::from("hello");

'''

The double colon _::_ operator allows us to namespcae this particular _from_ function under the _String_ type rather than using some sort of name like string_from.

This type of string can be mutated:

'''

let ,ust s = String::from("hello");

s.push_str(", world"); // push_str() appends a literal to a String

println!("{}", s); // This will print _hello, world_.

'''

Why can String be mutated and literals cannot? Difference is in how these two types deal with memory.

---------------

## Memory Allocation:

With the _String_ type, in order to support a mutalbe, growable piece of text, we need to allocate on amount of memory on the heap, unknown at compile time, to hold the contents.

This means:

* The memory must be requested from memory allocator at runtime.

* We need a way of returning this memory to the allocator hen we're done with our String.

First part is done by us when we call _String::from_, its implementation requests the memory it needs.

Second part is different. The memory is automatically returned once the vairable that owns it goes out of scope.

Eg. 

'''

let s = String::from("hello");

// _s_ is valid from this point forward

// do stuff with _s_.

}

// This scope is now over, _s_ is no longer valid.

'''

-----------

There is a natural point at which we can return the memory our String needs to allocator: when _s_ goes out of scope. When a variable goes out of scope, Rust calls a special function _drop_. Rust calls _drop_ automatically at the closing curly brackets.

In c++, this pattern of deallocating resources at the end of an item's lifetime is called Resouce Acquisition Is Initialization(RAII). The _drop_ function is similar.

This pattern has a profound impact on the way Rust code is written. The behaviour of code can be unexpected in more compmlicated situations when we want to have multiple variables use the data we've allocated on the heap.

----------

## Variables and Data Interacting with _Move_:

Multiple variabels can interact with same data in different ways in Rust.

Eg. 

'''

let x = 5;

let y = 5;

'''

--------------

Bind 5 to _x_ then make a copy of value in _X_ and bind it to _y_.

Integers are simpler values with a known fixed size and these two 5 values are pushed on the tack.

Similarly:

'''

let s1 = String::from("hello");

let s2 = s1;

'''

------

This looks similar to above example but does not work in same fasion.

