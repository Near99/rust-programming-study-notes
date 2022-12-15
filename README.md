# The Rust Programming Language Study Notes.

## Chapter 1

### Cargo

- Rust's build system and package manager.

- Cargo's configuration format is TOML which stands for Tom's Obvious, Minimal Language.

- <code>cargo run</code> will build the source file and execute it.

- <code>cargo check</code> quickly checks the code to make sure it compiles but doesn't produce an executable.

- <code>cargo build --release</code> build release version with optimizations.


## Chapter 3

### Mutability

- Variables are immutable by default.

```rust
let x = 10; // unable to reassign value.
```

- Add <code>mut</code> keyword before variable name to create mutable variables. 

```rust
let mut y = 10;
println!("The value of y is: {y}");
y = 20;
println!("The value of y is: {y}");
```

### Constants

#### Difference between constants and variables

1. Cannot use <code>mut</code> with constants.

2. Type of the value must be annotated.

3. Constants can be declared in any scope.

4. Constants may be set only to a constant expression, not the result of a value that could only be computed at runtime. (??)

### Shadowing

- It is able to declare a new variable with the same name as a privious variable.

```rust
let x = 5;
let x = x * 20;
{
    // First two xs are shadowed by the third x.
    let x = x * 2;
    println!("The value of x is: {x}"); // 200
}

let space = "     ";
let space = space.len();
println!("The length of space is: {space}"); // 5
```

### Data Types

#### Scalar Types

- A scalar type represents a single value. There are four primary scalar types in rust: integers, floating point, booleans, characters.

1. Integers can be explicitly declared bit length 8, 16, 32, 64, 128 with prefix i(signed) or u(unsigned). Using isize, usize to automatically allocate bit length depends on architecture (32 or 64).

2. Floating-Points: f32, f64. Default is f64, and floating point is always signed.

3. Booleans: true or false, one byte in size.

4. Characters: char literals use single quotes same as cpp, but char in rust is four bytes in size represents Unicode Scalar Value rather than ASCII.
