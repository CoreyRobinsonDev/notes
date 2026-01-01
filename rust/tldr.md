# Variables
- _variable_ bindings are immutable be default
- use `mut` to declare a _variable_ as mutable
```rust
let x;
x = 42;
```
```rust
let x: i32 = 42;
```
-  use `_` to ignore the returned value of an expression
```rust
let _ = 42; // this does nothing because 42 is a constant

let _ = get_stuff(); // this calls get_stuff() and throws away its result
```
# Tuples
```rust
let pair = ('a', 17);
pair.0; // a
pair.1; // 17
```
```rust
let pair: (char, i32) = ('a', 17);
```
- _tuples_ can be destructured
```rust
let (some_char, some_int) = ('a', 17);
```
# Functions
```rust
fn greet() {
    println!("Hello, World!");
}
```
```rust
fn get_num() -> i32 {
    4
}
```
-  _functions_ can be generic
```rust
fn foobar<T>(arg: T) { ... }
```
# Structs
```rust
struct Number {
    odd: bool,
    value: i32
}
```
- _structs_ can be initialized using literals
```rust
let x = Number { odd: false, value: 2 };
```
- _structs_ can be generic
```rust
struct Pair<T> {
    a: T,
    b: T
}
```
```rust
let p1 = Pair { a: 3, b: 5 };
let p2 = Paor { a: true, b: false };
```
## Methods
```rust
struct Number {
    odd: bool,
    value: i32
}

impl Number {
    fn is_positive(self) -> bool {
        self.value > 0
    }
}
```
# Match
- _match_ arms are patterns
- arms are exhaustive
- use `_` as a catch all
```rust
fn print_num(n: Number) {
    match n.value {
        1 => println!("one"),
        2 => println!("two"),
        _ => println!("{}", n.value),
    }
}
```
# Vectors
```rust
let mut v1 = Vec::new();
v1.push(1);
let mut v2 = Vec::new();
v2.push(true);
```
- use the macro `vec![]` to initialize vector literals
```rust
fn main() {
    let v1 = vec![1, 2, 3];
    let v2 = vec![true, false, true];
}
```
# Iterators
```rust
// 0 or greater
(0..).contains(&100); // true
// 20 or less
(..=20).contains(&20); // true
// only 3, 4, 5
(3..6).contains(&4); // true
```
