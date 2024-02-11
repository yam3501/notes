# Control flow

The ability to run some code based on whether a condition is _true_ and to run some code repeatedly while a condition is _true_ are basic building blocks in most programming languages. The most common consructs that let you control the flow of execution of Rust code are _if_ expressions and _loops_.

---------------

## "if" Expressions:

"if" expression allows you to branch your code depending on the conditions.

Eg.

'''
fn main(){

let no = 3;

if no < 5 {

println!("true");

} else {

println!("false");

}

}

'''
Error: expected 'bool'
-----------

Conditions in this code must be a "bool".

---------

### Handling Multiple Condtions with "else if":

Eg.

'''

fn main(){

let no = 6;

if no%4 == 0{

println!("divisible by 4");

} else if no%3 == 0 {

println!("divisible by 3");

} else if no%2 == 0 {

println!("divisible by 2");

} else {

println!("not divisible by 4, 3, or 2");

}

}

'''

--------------------

Even though 6 is divislbe by 2, we won't see output "divisible by 2", Rust only executes the block for first "true" condition.

---------------

### Using if in a let Statement:

Eg.

'''
fn main(){

let condition = true;

let no = if condition {5} else {6};

println!("{no}");

}

'''

-------

"no variable will be bound to value based on results from each arm of "if" must be the same type.

------------

## Repetition with Loops:

Rust has three kinds of loops:-

'loop', 'while', and 'for".

_loop_ keyword tells Rust to execute a block of code over and over again until you explicitly tell it to stop.

Eg.

'''
fn main(){

loop{

prinln!("again!");

}

}

'''

-----------------------

We'll see _again!_ printed over and over continuously until we hit _^c_.

You can place _break_ keyword within the loop to tell the program to stop executing the loop.

We can also use _continue_ to skip over any remaining code in this iteration of loop and go to next iteration.

------------

### Returning Values from _loops_:
Eg.

'''
fn main(){

let mut counter = 0;

let result = loop{

counter += 1;

if counter == 10 {

break counter * 2;

}

};

println!("{result}");

}

'''

-------------------

### Loop Labels to Disambiguate Between Multiple Loops:

If you have loops within loops, break and continue apply to innermost loop at that point.

Optimally you can specufy a loop label that you can use with _break_ and _continue_ to specify that those kewqords apply to the labeled loop instead of innermost loop.

Loop labels must begin with a single quote.

Eg.

'''
fn main(){

let mut count = 0;

'counting_up': loop {

println!("count = {count}");

let mut remaining = 10;

loop{

println!("remaining = {remaining}");

if remaining == 9 {

break;

}

if count == 2{

break 'counting_up;

}

remaining -= 1;

}

count += 1;

}

println!("end count = {count}");

}

'''

$ cargo run
count = 0
remaining = 10
remaining = 9
count = 1
remaining = 10
remaining = 9
count = 2
remaining = 10
end count = 2

------------

The first break that doesn't specify a label will exit the inner loop only.

The _break_ 'counting_up' will exit outer loop.

--------------

## Conditional Loops with _while_:

Eg.

'''
fn main(){

let mut number = 3;

while number != 0 {

println!("{number}!");

number -= 1;

}

println!("LIFTOFF!!!");

}

'''

---------------

This contruct eliminates a lot of nesting that would be necessary if you used _loop_, _if else_, and _break_.

While a condition evaluates to true, code runs, otherwise, it exits the loop.

-----------

##Looping Through a Collection with _for_:

You can choose to use while_ over elements of collection such as an array.

Eg.

'''
fn main(){

let a = [10, 20, 30, 40, 50];

let mut index = 0;

while index < 5{

println!("value is:{}, a[index]);

index += 1;

}

}

'''

----------

However, this approach is error prone.

For example, if you changed definition of 'a' to have four elements but forgot to update the condition to _while index < 4_, code would panic.

It's also slow, because compiler adds runtime code to perform the conditional check of whether index is within bounds on array on every iteration.

_for_ loop is more concise alternative.

Eg.

'''
fn main(){

let a = [10, 20, 30, 40, 50];

for element in a {

println!("value is: {element}");

}

}

'''

---------

To do the countdown example with _for_, we use a range, provided by the standard library, which generates all numbers in sequence starting from one number and ending for another number.

Eg.

'''
fn main(){

for number in (1..4).rev(){

prinln!("LIFTOFF!!!");

}

'''

------------

