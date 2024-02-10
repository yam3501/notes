# Data Types

Rust is a statistically typed language, which means that it must know the types of variables at compile-time.

------------------------

## Scalar Types:

A scalar type represents a single value. Rust has 4 primary scalar types: integers, floating-point numbers, booleans and characters.

-------------------

### Integer Type:

An integer is a number without a  fractional component.

'''
length 		Signed 	unsigned
8 bit		i8		u8
16 bit 		i16 	u16
32 bit 		i32  	u32
64 bit 		i64		u64
128 bit 	i128	u128
'''

Signed and unsigned refers to whether it's porssible for the number to be negative.
Each signed variant can store numbers from -(2^(n-1)) to 2^(n-1)+1 inclusive, where n is the number of bits.

So, i8 can store numbers from -2^7 to 2^(7)-1. Which equals -128 to 127.

Unsigned variants can store numbers from 0 to 2^(n-1). So, u8 can store numbers from 0 to 2^(8-1) which is 0 to 255.

---------------------

The isize and usize types depend on the architecture of the computer your program is running.

---------------

Number literals that can be multiple numberic types allow a type suffix -> 57u8 to designate the type.

Number literals can also use an underscore as a visual separator to make number easier to read.

-------------

The primary situation in which you'd use isize & usize is when indexing some kind of collection.

---------------

### Floating-Point Type:

Rust's floating point types are f32 and f64, which are 32-bit and 64-bit in size.
The default type is f64 because of modern CPUs, it is roughly same speed as f32 but is capable of more precision.

---------------

All floating point numbers are signed

------------

Eg.

'''
fn main(){
	let x = 2.0; // f64
	let y : f32 = 3.0; //f32
}
'''

-------------

Floating point numbers are represented according to IEEE-754 standard.

f32 is a single-precision float and f64 is a double precision float.

----------------------

### The Boolean Type:

The boolean type in Rust has two possible values: "true" and "false".

Booleans are one byte in size.

Boolean type in Rust are specified using "bool".

Eg.

'''
fn main(){
	let t = true;
	let f:bool = false; // with explicit annotation
}
'''

---------------

The main way to use boolean values is through conditionals, such as if expression.

--------------------

### The Character Type:

Rust's "char" type is the language's most primitive alphabetic type.

Eg.

'''
fn main()
{
	let c = 'z';
	let z:char = 'z'; // with explicit annotation
	let smile = '☺';
}
'''

---------

We specify "char" types with single quotes as opposed to string literals, which use double quotes.

Rust's "char" type is 4 bytes in size and represents a Unicode Scalar Value, which means that it can represent a lot more than just ASCII. Accented letters, Chinese, Japanese, and Korean characters, emoji, and zero-width spaces are all valid "char" values in Rust.

Unicode Scalar Vlaues range from U+0000 to U+D7FF and U+E000 to U+10FFFF inclusive.

-------------

## Compound Types:

Compound types can group multiple values into one type. Rust has two primitive compound types: tuples and arrays.

-----------

### The Tuple Type:

A tuple is a general way of grouping together a number of values with a variety of types into a compound type.

Tuples have a fixed length: once declared, they cannot grow or shrink in size.

Eg.

'''
fn main()
{
	let tup:(i32, f64, u8) = (500, 6.4, 1);
}
'''

-------------

The variable tup binds to the entire tuple because a tuple is considered a single compound element. To get the individual values out of a tuple, we can use pattern matching to destructure a tuple value.

Eg.

'''
fn main(){
	let tup = (500, 6.4, 1);
	let (x, y, z) = tup;
	println!("The value of y is: {y}");
}
'''

------------

This program first creates a tuple. Then it uses a pattern with "let" to take tup and turn it into three separate variables: x, y, z.
This is called _Destructuring_ because it breaks the tuple into three parts.
Then finally prints the values of 'y'.

We can also accessa tuple element directly by using a period "." followed by index of value we want to access.

Eg.

'''
fn main(){
	let x:(i32, f64, u8) = (500, 6.4, 1);
	let five_hundred = x.0;
	let one = x.2;
}
'''

----------

Indexing in tuple starts from 0.

The tuple without any values has a special name "unit". This value and its corresponding type are both written () and represent an empty value or an empty return type. Expressions implicitly return the unit value if they don't reutrn any other value.

--------------

### The Array Type:

Unlike tuple, every element of an array must have the same type.

Arrays in Rust have a fixed length.

Eg.

'''
fn amin(){
	let a = [1, 2, 3, 4, 5];
}
'''

-----------

Arrays are useful when you want your data allocated on the stackrather than the heap or when you want to ensure you always have the fixed number of elements.

Array isn't as flexible as vector type.
A vector type is a similar collection type provided by the standard library that is allowed to grow or shrink in size.

Arrays are useful when you know the number of elements will not need to change.

Eg.

'''
	let months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
'''

You write an arrays type using square brackets with the type of each element, a semicolon and then the number of elements in the array.

Eg.

'''
	let a: [i32; 5] = [1, 2, 3, 4, 5];
'''

------------

You can also initialize an array to contain the same value for each element by specifying the initial value, semicolon, length of array in square brackets.

Eg.

'''
	let a = [3; 5];
	// which is same as 
	let b = [3, 3, 3, 3, 3];
'''

-----------------

#### Accessing Array Elements:

An array is a single chunk of memory of a known, fixed size that can be allocated on the stack.

You can access elements of array using indexing.

Eg.

'''
	let a = [1, 2, 3, 4, 5];
	let first = a[0];
	let second = a[1];
''' 

------------

#### Invalid Array Element Access:

Eg.

'''
	let a = [1, 2, 3, 4, 5];
	let last = a[5];
	println!("{last}");
'''

Error: index out of bounds.

------------

The program resulted in a runtime error.
When you attempt to an element using indexing, Rust will check that the index value you have specified is less than the array length.

If the index is greater than or equal to the length, Rust will panic.

This check has to happen at runtime, especially when the compiler doesn't know what value the user will input when they run the code later.

This is an example of Rust's memory safelty principles. In many low-level languages, this kind of check is not done, and when you provide an invalid index invalid memory can be accessed.

Rust protects you against this kind of error immediately exiting instead of allowing the memory access and continuing.

---------------

