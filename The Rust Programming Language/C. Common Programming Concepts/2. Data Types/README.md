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