# Functions:

Rust uses snak case as the onventional style for function and variable names, in which all letters are lowercase and underscores separate words.

Eg.

'''
fn main(){
println!("hello");
another_function();
}

fn another_function(){
println!("another");
}
'''

----------------

Rust doesn't care where you define your fnuctions, only that they are defined somewhere in scope where it can be seen by the caller.

The lines execute in order in whcih they appear in the main function.

--------------

## Parameters:

Eg.

'''
fn main(){
func(5);
}

fn func(x: i32){
println!("{x}");
}

'''
$ cargo run
-> 5
------------

