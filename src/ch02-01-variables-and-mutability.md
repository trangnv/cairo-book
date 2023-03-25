# Variables and Mutability

By default, variables are immutable. This is one of many nudges Cairo gives you to write your code in a way that takes advantage of the safety and easy concurrency that Cairo offers. However, you still have the option to make your variables mutable. Let’s explore how and why Cairo encourages you to favor immutability and why sometimes you might want to opt out.

When a variable is immutable, once a value is bound to a name, you can’t change that value. To illustrate this, generate a new project called variables in your projects directory by using `scarb new variables`

Then, in your new variables directory, create `src/main.rs` and fill with the following code, which won’t compile:

```rust
fn main() {
    let x = 5;
    debug::print_felt252(x);
    x = 6;
    debug::print_felt252(x);
}
```

Save and run the program using `cairo-run --path src/main.cairo`. You should receive an error message regarding an immutability error, as shown in this output:

```bash
error: Cannot assign to an immutable variable.
 --> main.cairo:4:5
    x = 6;
    ^***^

Error: failed to compile: src/main.cairo
```
