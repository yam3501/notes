## Creating a Project with Cargo

$ cargo new <project-name>


Project directory consists of 2 files and one directory: Cargo.toml file and a src directory with a main.rs inside
Also contains a new Git repository with a gitignore file

------------------------------

-> Cargo.toml is in the TOML(Toms's Obvious, Minimal Language) format. Cargo's configuration format.
-> [package] is a section heading that the following statements are configuring a package.
-> [dependencies] is a section where you ist all the project dependencies.

------------------------------

In Rust, packages are of code are referred to as "crates".

------------------------------

Cargo expects your source files should live inside the src directory. Top-level project directory is only for README files, License information, and anything else not related to the code.

------------------------------

## Building and running a Cargo Prpject

from the <project-name> directory, run the following command: 

'''
$ cargo build
'''

This command creates an executable file in the target/debug/<project-name>.exe
The default build is a debug build.
Running 'cargo build' for the first time causes cargo create a new file "Cargo.lock" at the top level.

------------------------------

To compile the code and run the resultant executable all in one command:

'''
$ cargo run
'''

------------------------------

To check whether the code compiles but doesn't create an executable:

'''
$ cargo check
'''
 faster than 'cargo build' because it skips the step of producing executable.

------------------------------

When project is ready for release, use:

'''
$ cargo build --release
'''

This will create the executable in target/release instead of target/debug


