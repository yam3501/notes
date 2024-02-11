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

The lines execute in order in which they appear in the main function.

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

5
------------

In functions signatures, you must decalre each parameter type.

When defining multiple parameters, separate the parameter declarations with commas.

-------------

## Statements and Expressions:

_Statements_ are instructions that perform some action and do not return a value.

_Expressions_ evaluate to a resultant value.

Creting a variable and assigning a value to it with the "let" keyword is a statement.

Function definitions are also statements.

Statements do not return values.

Expressions evaluate to a value and can be part of statements.

Calling a function, calling a macro, a new scope block created with curly brackets are all expressions.

Eg.

'''
fn main(){

  let y = {
  
    let x = 3;
    
    x + 1
    
  };
  
  prinln!("{y}");
  
}
'''

The expression

{

  let x = 3;
  
  x + 1
  
}
evaluates to 4. That gets bound to y as part of "let" statement.

Expressions do not include ending semicolons.

-------------

## Functions with Return Values:

Functions can return values to the code that calls them.

Eg.

'''
fn five(){

  5
  
}

fn main(){

  let x = five();

  println!("{x}"};

}

'''

Eg. 

'''
fn main(){

  let x = plus_one(5);

  println!("{x}"};

}

fn plus_one(x: i32) -> i32{

  x + 1

}

'''

----------------

If we place a semicolon at end of "x + 1", changing it from expression to statement, we'll get an error.

----------------

