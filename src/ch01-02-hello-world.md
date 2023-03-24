# Hello, World!

## Creating a Project Directory

## Writing and Running a Cairo Program

```bash
mkdir ~/projects
cd ~/projects
mkdir hello_world
cd hello_world
```

- Create new file `main.cairo` and add the following code:

```rust
fn main() {
    debug::print_felt252('Hello, world!')
}
```

- Save the file and go back to your terminal window in the ~/projects/hello_world directory. On Linux or macOS, enter the following commands to compile and run the file:

```bash
cairo-run --path main.cairo
```

The string Hello, world! should print to the terminal, with some other information that we don't really need to care for now.

Congratulations! You’ve officially written a Cairo program. Welcome to the world of Cairo!
