
# Rust Programming Language

## Hello World

```rust
fn main(){
	println!("Hello World!");
}
```

## Ch. 0

### About
This section is for the who, what, where, when, why and how of Rust. 

### Basics
Rust has a list of keywords that we cannot use as variable names and such. You can see them all in [Appendix A](https://doc.rust-lang.org/book/appendix-01-keywords.html). 

Variable declaration use keywords ```let``` and ```const```.
```rust
const VAR_NAME: u32 = 1;
fn main() {
	let mut var_name: i32 = 0;
}
```
Constants are like regular variable declarations but cannot be made mutable and can be declared in the global name space. 

You can redeclare variables, even if if they aren't mutable, in a process called **shadowing**. Shadowing is much different than reassigning with mutability. 
```rust
fn main(){
	let x = 5;
	let x = x + 1;
}
``` 
## Data Types
Rust is a _statically typed language_, which means Rust needs to know the data types of the variables at compile time. However, the compiler usually infer what type we want to use based on the value and how we use it. 

**Scalar Types** represent a single value. Rust has 4 main scalar types: integers, floats, Booleans, and characters. 
Length | Signed | Unsigned
:-|:-:|:-:
8-bit | i8 | u8
16-bit | i16 | u16
32-bit | i32 | u32
64-bit | i64 | u64
128-bit | i128 | u128
arch | isize | usize

```rust
fn main(){
	let x: i16 = "24".parse().expect("Not a number!");
}
```
If you save a value in a variable to cause integer overload, the compiler will _panic_ in debug mode. If you compile in _release_ mode, with the ```--release``` flag, Rust performs _two's complement wrapping_, which means the value will wrap around, back to **0**. 

Rust floating points come in 2 flavours, ```f32``` and ```f64```.

#### Numeric Operations 
[+ - * / %]

We also have a **Boolean** type. 
```rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```

There's also the ```char``` type. These are denoted with only single quotes. The string literals are written in double quotes. 

**Compound Types** can group multiple values into one type. 

**The Tuple Type** can group together multiple different types, but have a fixed length, they cannot grow or shrink.

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
The variable is bound to the entirety of all values. 

You can destructure tuples. 

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;
    println!("The value of y is: {y}");
}
```
You can access a tuple element directly with dot notation, using a period, followed by the index value we want access. Rust is a **0** indexed language, like all the rest. 
```rust
fn main() {
	let x: (i32, f32, u8) = (100, 6.4, 1);
	let six_four = x.1;
}
```

A tuple without any values is called a _unit_. It's written, both type and values as `()`. 

### The Array Type
This is another collection of multiple values, but unlike a tuple, all of the values in an _array_ must be of the same type. _Arrays_ in **Rust** must also have a fixed length, as in some other languages. 
```rust
let x: [i32; 3] = [1,2,3];
```
Each element is an `i32` and the array is `3` elements long. There's also a way to create an array of duplicate elements, specify `[value, length]`. And you can use square brackets to access elements. 
```rust
fn main() {
	let a = [1; 3];
	let x = a[0];
}
```
You are unable to access elements beyond the scope of the array's length. If the index is not known at runtime, but later input by the user, the program will crash with a _runtime_ error. Basically, Rust will check if the index value is less than the length and **panic** if it's not. 
Don't take this check for granted, it's Rust's memory safe principles in action. And not all low-level languages run this check. This means that other languages allow for invalid memory to be accessed, a _memory leak_. 

### Functions

[Rust-lang/functions](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#functions)
The most important function is `main`, which is the entry point of the program. We create functions using the `fn` keyword. 
```rust
fn main() {
	do_more();
}
fn do_more(){
	println!("This is String");
}
```
Curly brackets lets the compiler know where the function begins and ends. Note that Rust doesn't care where the function is called and defined, as long the function is defined in a scope seen by the caller. 

#### Parameters
You can define a function with parameters. This allows the user to pass arguments into the function. 

```rust
fn main(){
	do_more(5);
}
fn do_more(x: i32, y:u16){
	println!("These are numbers: {x}, {y}");
}
```
In the function signature we _must_ declare the type for each parameter. This is deliberate by Rust. 

#### Statements and Expressions
Function bodies are made up of a series of statements and optionally ending in an expression. Rust is an _expression_-based language, so the distinction between statements and expressions is important. 
- Statements are instructions that perform an action and do not return a value. 
- Expressions evaluate to a resulting value. 

Function and variable declaration are statements. In other languages, declaring variables actually returns a value (like Ruby), but not in Rust. 
Mathematical operations, calling functions, and calling macros are expressions. You can create an expression by encapsulating logic in curly brackets. If you create an expression to return at the end of a function, you must leave off the semicolon. If you add a semicolon, it becomes a statement and will not return a value. 
```rust
fn add_one(x: i32) -> i32 {
	x+1
}
fn main(){
	let y = add_one(5);
	println!("The plus one: {y}");
}
```

#### Functions with Return Values
As seen in the above example, we _must_ declare the return type using an arrow `->`. In Rust, the return value of a function is synonymous with the final expression in said function. You can also return early from a function using the `return` statement. 

We can also use the return value of a function to initialize a variable. The compiler can usually figure out the type of the variable based on the return type of the function. 

Note that if the last line of a function is an expression with a semicolon, it becomes a statement and thus returns nothing. This will cause the compiler to panic. 

### Comments
Use `//` to initiate a comment. Usually they are written above a piece of code, but you can include them at the end of a line as well.

### Control Flow
[Control Flow](https://doc.rust-lang.org/book/ch03-05-control-flow.html#control-flow)

The most common constructs that allow you to control the flow of code are the conditional `if` expressions and loops. 

#### if expressions

They are called expressions because they can return a value. The if-expression begins with the `if` statement, followed by a condition. If the condition evaluates to `true`, then Rust will evaluate the code within the curly braces. Else, it will move to the next line block.

In the below example, the next block is an `else if` statement, with another conditional. The conditional is only checked if the first test evaluated to false. You can have many `else if` blocks; however, there are other means to this end as well.

```rust
fn main(){
	let val: i16 = 5;
	if val < 10 {
		println!("Number less than 10");
	} else if val == 10 {
		println!("Number is 10");
	} else {
		println!("Number greater than 10");
	}
}
```

Finally, there's the `else` expression. This is like the "catch-all" if all conditionals above it, in the same block/scope, evaluated to `false`. The `else` statement is optional; you could easily leave nothing there. 

Other programming languages allow values to be evaluated to `true`. It is worth noting that in Rust, the conditional must evaluate to a `bool` type. If you try to use just, say for example, an integer value, you will get an error that Rust was expecting a `bool` type. Rust is more explicit than other languages and will not convert non `bool` type to Boolean. 

#### Using `if` in a `let` statement

Because `if` is an expression, we can use it on the right of a `let` statement to assign a variable conditionally.

```rust
fn main(){
	let condition = true;
	let val: i16 = if condition {10} else {5};
}
```

From other programming languages, this may resemble a ternary operation. Remember that Rust needs to know a variable's type at compile time. If you mis-match types in the conditional then Rust will throw an error during compilation. 

#### Repetition with loops

Rust has three loop keywords: `loop`, `while`, and `for`.

The `loop` keyword tells Rust to execute a block of code until explicitly told to stop. This is where we can introduce the `break` and `continue` keywords as well. These, used with conditionals, can help to escape parts of code within a loop, or the loop itself. 

```rust
fn main(){
	let mut counter: i32 = 0;
	let result = loop {
		if counter >= 10 {
			break counter + 3;
		} else if counter < 5 {
			counter += 1;
			continue;
		} else {
			counter += 1;
		}
		counter += 1;
	}
	
}
```

Just like for conditional, loops are also expressions, and their results can be stored in a variable. You might use something like this for a process that is waiting on another process, and break out of the loop when the waiting is complete. Note that the `continue` statement/expression is meant to skip the rest of the code below and kick-off the next iteration of the loop.

Additionally, the `break` keyword acts almost like the `return` keyword in a function. You can return values from a `loop`, making it an expression, by tagging them to the end of the `break` keyword. 

Also, the value of `counter`  is still available after the looping is complete. **Ownership** is a topic for later, but values passed along are typically destroyed. However, a loop does not appear to own or destroy any values, just like the `if` expression. 

##### Loop Labels to Disambiguate between multiple loops
[@here](https://doc.rust-lang.org/book/ch03-05-control-flow.html#loop-labels-to-disambiguate-between-multiple-loops)
If you have loops within loops, the `break` and `continue` statements work on the innermost loops. We can specify a _loop label_ to use those keywords on a labelled loop instead of the innermost loop. You apparently use just one single-quote to declare the label. 
```rust
fn main(){
	let mut outer_count = 0;
	'counting_up: loop {
		println!("Outer count = {outer_count}");
		let mut inner_count = 10;
		loop {
			if inner_count == 9 {
				break;
			}
			if count == 2 {
				break 'counting_up;
			}
			inner_count -= 1;
		}
		outer_count += 1;
	}
	println!("Ending count = {outer_count}")
}
```

The above code loops and counts down, and then up, until breaking out. 

##### Conditional Loops with While

A `while` loop will run while its condition evaluates to `true`. When the condition evaluates to `false`, the program calls `break`, stopping the loop. 

```rust
fn main(){
	let mut count_down = 3;
	while count_down != 0 {
		println!("{count_down}");
		count_down -= 1;
	}
	println!("Blast off!");
}
```

##### Conditional Loops with For

A `for` loop is best used on iterables like arrays or a range. We haven't covered the `rev()` method for a range yet, but it's obvious what it does.
```rust
fn main(){
	for number in (1..4).rev() {
		println!("{number}");
	}
	println!("Blast Off!");
}
```

### Summary

We have covered a bit. A good test of skill is to create a program that prints the nth Fibonacci number. 

## Ch. 4 - Ownership

**Ownership** is an important topic in how Rust manages memory. We will also cover the topics of _borrowing_, _slices_, and how data is laid out in memory. 

### What is Ownership?

[@Ownership](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#what-is-ownership) is "... a set of rules that governs how a Rust program manages memory." Some programs use "garbage collectors", and others leave it up to the programmer to explicitly allocate and free memory. Rust uses the _ownership_ method which is a set of rules that the compiler checks, and if any rules are violated the program won't compile. The features of ownership won't slow down your program while it is running. 

To understand ownership, we must discuss how memory is managed in the _stack_ and in the _heap_. Depending where a value is located in memory, will determine how it interacts with other parts of your program. 

### Stack

The **stack** is like a container of memory that stores values in the order it gets them and removes them in the opposite order. IT is _last in, first out_, or LIFO. You can think of it like a stack of plates. To add to the stack, we push a plate on, and to remove, we pop a plate off. Data stored on the stack must have a known-fixed size at compilation. Data with and unknown size when compiled will be allocated to the heap. 

### Heap

The **heap** is less organised than the stack. When memory needs to be allocated to the heap, the program requests memory with a certain size. The memory allocator finds a space, reserves it for the program, and returns a _pointer_. This process is referred to as "allocating to the heap". The pointer, being a known fixed size, can be store on the stack. 

Pushing to the stack is quicker than allocating to the heap. Allocating to the heap also requires much more work to be done for both storing and retrieving data. Retrieving data is also slower because the program has to follow a pointer. When the code calls a function, the arguments passed in and the function's local variables are pushed to the stack. And once the function is finished executing, the values get popped off. Ownership helps to minimize duplicate data and clean up space on the stack and heap, removing unused data. 

### Rules of Ownership

- Each value in **Rust** has an _owner_. 
- Each value can only have one _owner_ at a time. 
- When a function goes out of scope, the value is dropped. 

### Variable Scope

Let's look at a quick example.

```rust
fn main() {
	let s = "Hello, world!";
	println!("Hello");
}
```

[@here](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#variable-scope)

The **scope** is the range in a program in which the variable is valid. The variable declared as `s` is a string literal. It has two main points of time, when it is declared and brought into scope, and when it goes out of scope. Apparently this is where we can introduce a `String` type. 