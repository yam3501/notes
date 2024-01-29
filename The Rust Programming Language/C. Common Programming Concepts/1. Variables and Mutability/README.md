## Variables and Mutability:- 

By default, variables are immutable. However you still have option to make variables mutable.
When a variable is immutable, once a value is bound to a name, you can't change that value.

Eg.

'''
fn main(){
   let x = 5;
   println!("The value of x is: {x}")'
   x = 6;
   println!("The value of x is: {x}");
}
'''

Error: cannot assign twice to immutable variable 'x'

-----------------------

Mutability can be very useful. You can add "mut in front of variable name to make it mutable."

Eg.

'''
fn main(){
   let mut x = 5;
   println!("{x}");
   x = 6;
   println!("{x}");
}
'''

-> $ cargo run

5

6

We're allowed to change the value bound to x from 5 to 6 when "mut" is used.

---------------------------

# Constants:

Like immutable variables, constants are values that are bound the a name and are not allowed to change.

"mut" can't be used with constants. Constants are always immutable.

You declare constants with the "const" kewor instead of "let" keyword and value must be annotated.

Constants can be declared in any scope, including global scope, which makes them useful for values that may be parts of code need to know about.

Constants may be set only to a constant expression, not the result of a value that could only be calculated at runtime.

Eg. 

'''
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
'''

----------------------------

Rust's naming convention for constants is to use all uppercase with underscores between words.

Constants are valid for entire time a program runs, within the scope in which they were declared.

Naming hardcoded values used throughout your program as constants is useful in conveying the meaning of that value to future maintainers of the code.

It also helps to have only one place in your code you would need to change if the value needed to be updated in future.

-------------------------

# Shadowing:

You can declare a new variable with the same name as a previous variable.
It is said that the first variable is 'shadowed' by the second, which means that the second variable is what the compiler will see when you use the name of the variable.
In effect, the second variable overshadows the first, taking any uses of the variable to itself until it itself is shadowed or the scope ends.

Eg. 

'''
fn main(){
   let x = 5;
   let x = x + 1;
   {
      let x = x * 2;
      println!("{x}");
   }
}
'''

-> $ cargo run

12

6

---------------------------

The program first binds x to value 5. Then creates a new variable x, taking the original value and adding 1 so value of x is 6.
Then within an iner scope "let" statement shadows x and creates a new variable, multiplying previous value by 2 to give x = 12.
When that scope is over, inner shadowing ends.
x = 6

---------------------

Shadowing is different from making a variable "mut" because we'll get compile-tim error if we accidently try to reassign this variable without using "let" keyword.

By using "let", we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.

Because we're creating a new variable when we use "let" keyword again, we can change the type of value.

However if we try to use "mut" for this, we'll get compile-time error

-> Error: mismatched types