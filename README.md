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
// This is good.
let x = 3;

// And this is cool.
let y: i32;
y = 1024;

// unable to reassign value.
x = 33; // error..
y = 2048 // error..
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

#### Scalar Types - represent a single value.

1. Integers can be explicitly declared bit length 8, 16, 32, 64, 128 with prefix i(signed) or u(unsigned). Using isize, usize to automatically allocate bit length depends on architecture (32 or 64).

2. Floating-Points: f32, f64. Default is f64, and floating point is always signed.

3. Booleans: true or false, one byte in size.

4. Characters: char literals use single quotes same as cpp, but char in rust is four bytes in size represents Unicode Scalar Value rather than ASCII.

#### Compound Types - group multiple values into one type.

##### Tuples - holds a number of values with variety of types.

* **Tuples are fixed in size once declared.**

- Declaration:

```rust
let tup: (i32, f64, bool, char) = (500, 20.5, false, 'w');
```

- Destructuring:

```rust
let tup: (i32, f64, bool, char) = (500, 20.5, false, 'w');
let (i, j, k, n) = tup;
```

- Direct access:

```rust
let tup: (i32, f64, bool, char) = (500, 20.5, false, 'w');
let i = tup.0;
let j = tup.1;
let k = tup.2;
let n = tup.3;
```

- Empty tuples are called unit.

```rust
let empty_tup = ();
```

#### Arrays - holds a number of values with the same type.

- Declaration:

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

- Initialize an array to contain the same value for each element.

```rust
let a = ["hello, world"; 5];
```

### Functions

- Function declaration above main is not required as if it is in C or C++.

- Types of all parameters must be declared.

#### Statements and Expressions - Rust is an expression based language

- **Statements are instructions that perfrom some action and do not return a value.**

- **Expressions evaluate to a resulting value.**

- Wrong, because statements do not return values, that is different from C and C++.

```rust
fn main() {
    let x = (let y = 6);
}
```

- Expressions do not include ending semicolons.

```rust
// yields 6
{
    let x = 5;
    x + 1
}
```

- Functions with return values must have return type declared.

- The return value of the function is synonymous with the value of the final expression in the block of the body of a function.

- Return value does not have to be named in rust, it will always return the last expression implicitly.

```rust
fn return_value() -> i32 {
    1024
}
```

- Using <code>return</code> keyword to return early with a specific value in the function.

```rust
fn return_early(x: i32) -> i32 {
    if x == 33 {
        return 512;
    }
    1024
}
```

### Control Flow

#### if

- Parentheses are not required in rust.

```rust
if 2 > 1 {
    println!("God damn it Gump You're a goddamn genius!");
}
```

- Conditions in if statements must be booleans, rust does not convert non-boolean types to a boolean automatically. 

```rust
// Cannot do this in rust.
let ch = 1;
if ch { 
    // do something..
}
```

#### Using if in let Statement

```rust
// No ternary in rust this is what it offers.
let x = if 2 > 1 { 2 } else { 1 };
```

#### Loops

##### loop

- <code>loop</code> must be explicitly stopped.

- <code>loop</code> is an expression that has return value, return value can be placed after <code>break</code> keyword.

```rust
let mut x = 10;
let y = loop {
    if x == 20 {
        break x * 2;
    }
    x += 1;
};
println!("{y}");
```

- loops can have labels, it is useful in nested loops to break the outer loop from the inner one.

```rust
let mut counter = 0;
'counter_loop: loop {
    println!("Counter is :{counter}");
    let mut remaining = 10;

    loop {
        println!("Remaining is :{remaining}");
        if remaining == 8 {
           break;
        } else if counter == 2 {
            break 'counter_loop;
        }
        remaining -= 1;
    }
    counter += 1;
}
```

##### while

- <code>while</code> is not much different from other languages except the parentheses are eliminated.

```rust
let mut x = 10;
while x >= 0 {
    println!("{x}");
    x -= 1;
}
```

##### for

- <code>for</code> is as clean as python, quite nice.

```rust
let arr = [10, 20, 30, 40, 50];

// loop through an array.
for n in arr {
    println!("{n}");
}

// loop a range of numbers.
for j in 0..10 { // equals to: for (int i = 0; i < 10; i++) {};
    println!("{j}"); 
}
```
