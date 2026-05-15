# Land of Rust: Ferris the Space Crab’s Adventures  
## Chapter 19: Opening the Spaceship Engine (Unsafe Rust and Macros)

### 📑 Chapter Index
[19.1. Serious Warning: This Is the Engine Room (unsafe)](#191-serious-warning-this-is-the-engine-room-unsafe)  
[19.1.1. Story: The Hot Spaceship Engine](#1911-story-the-hot-spaceship-engine)  
[19.1.2. What Is unsafe?](#1912-what-is-unsafe)  
[19.1.3. What Can You Do in unsafe?](#1913-what-can-you-do-in-unsafe)  
[19.1.4. Example: Raw Pointers](#1914-example-raw-pointers)  
[19.1.5. Calling an unsafe Function](#1915-calling-an-unsafe-function)  
[19.1.6. Exercise: Modifying a Raw Pointer](#1916-exercise-modifying-a-raw-pointer)  
[19.2. Making Your Own Magic (Macros)](#192-making-your-own-magic-macros)  
[19.2.1. Story: Ferris’s Magic Word](#1921-story-ferriss-magic-word)  
[19.2.2. What Is a Macro and How Is It Different from a Function?](#1922-what-is-a-macro-and-how-is-it-different-from-a-function)  
[19.2.3. The Simplest Macro with `macro_rules!`](#1923-the-simplest-macro-with-macro_rules)  
[19.2.4. Macros with Parameters (`ident`)](#1924-macros-with-parameters-ident)  
[19.2.5. Macros with a Variable Number of Arguments](#1925-macros-with-a-variable-number-of-arguments)  
[19.2.6. Commonly Used Macros in Rust](#1926-commonly-used-macros-in-rust)  
[19.2.7. Exercise: The `easy_vec!` Macro](#1927-exercise-the-easy_vec-macro)  
[19.3. Project: Building the `repeat!` Macro](#193-project-building-the-repeat-macro)  
[19.3.1. Goal](#1931-goal)  
[19.3.2. Implementing `repeat!`](#1932-implementing-repeat)  
[19.3.3. Testing the Macro](#1933-testing-the-macro)  
[19.4. Summary and Challenge](#194-summary-and-challenge)  
[19.4.1. Concept Review](#1941-concept-review)  
[19.4.2. Challenge: The `create_function!` Macro](#1942-challenge-the-create_function-macro)  

---

### 19.1. Serious Warning: This Is the Engine Room (unsafe)

#### 19.1.1. Story: The Hot Spaceship Engine
Deep inside Ferris’s spaceship there is a heavy metal door with red writing: `⛔ Danger! Senior engineers only`. Behind this door works the main engine. The temperature is extremely high, and if someone enters without training, everything might explode! 💥  
In the Rust world, most of the time we work in the safe parts (**Safe Rust**), where the compiler acts like a kind guard and checks all the rules so we don’t make mistakes. But sometimes, for very special tasks (like talking directly to hardware or using old C libraries), we have to enter the `unsafe` room.  
**Learning `unsafe` means you understand where Rust’s real power lies – but like a wise wizard, you only use it when absolutely necessary.** 🧙‍♂️

> 👨‍👩‍👧 **Note for parents and teachers**  
> `unsafe` is one of the most advanced topics in Rust and is rarely used in ordinary programs. The goal of this chapter is to introduce its existence, not to encourage its use. The official Rust book has a full chapter on `unsafe`:  
> [doc.rust-lang.org/book/ch19-01-unsafe-rust.html](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html)

#### 19.1.2. What Is unsafe?
`unsafe` is a keyword that tells the compiler: “Friend, I’ll take care of memory safety here myself. Please turn off your checks so I can do my job.”  
⚠️ **Golden tip:** `unsafe` does **not** mean “unsafe”! It means the compiler won’t enforce its usual rules, but you must act like a professional engineer and make sure you don’t corrupt the data. Only use it when you really have no other choice!

```rust
unsafe {
    // here we can do low‑level things
}
```

#### 19.1.3. What Can You Do in unsafe?
Inside an `unsafe` block, five things become allowed that are forbidden in normal code:
🔹 Dereferencing **raw pointers** (`*const T` and `*mut T`)  
🔹 Calling **unsafe functions** (usually C functions)  
🔹 Modifying mutable static variables (`static mut`)  
🔹 Implementing **unsafe traits**  
🔹 Accessing fields of a `union`

#### 19.1.4. Example: Raw Pointers
In normal Rust we use `&` and `&mut`, which are always safe and valid. But raw pointers (`*const T` and `*mut T`) can point to any address (even zero or `null`). The compiler cannot check whether that address is valid, so we are only allowed to read or write through them inside `unsafe`:
```rust
fn main() {
    let mut num = 5;

    // creating raw pointers (this is not unsafe, we are just taking addresses)
    let r1 = &num as *const i32;
    let r2 = &mut num as *mut i32;

    // reading or writing through a raw pointer must be inside unsafe
    unsafe {
        println!("Value of r1: {}", *r1); // 5
        *r2 = 10; // change the value through the pointer
        println!("New value of r2: {}", *r2); // 10
    }
}
```

#### 19.1.5. Calling an unsafe Function
Some functions in Rust are marked `unsafe`. To call them you must be inside an `unsafe` block. A common use is communicating with C code (called FFI):
```rust
extern "C" {
    fn abs(input: i32) -> i32; // absolute value function from the C library
}

fn main() {
    let x = -5;
    unsafe {
        println!("The absolute value of {} is {}", x, abs(x)); // 5
    }
}
```

#### 19.1.6. Exercise: Modifying a Raw Pointer
Create a mutable `i32` variable with the value `42`. Create a raw pointer `*mut i32` to it. Inside an `unsafe` block, change its value to `100` and print it.

💡 **Sample answer:**
```rust
fn main() {
    let mut value = 42;
    let raw_ptr = &mut value as *mut i32;

    unsafe {
        *raw_ptr = 100;
        println!("New value: {}", *raw_ptr);
    }
}
```

![[Illustration: Cartoon spaceship engine room with glowing warning signs labeled "unsafe". Ferris wears a protective engineer suit and helmet, carefully turning a glowing valve labeled "*mut T". Steam and soft blue energy fill the room. Style: dramatic but child-friendly, high contrast, vibrant children's book illustration, 16:9.]](../assets/images/19.1.png)

---

### 19.2. Making Your Own Magic (Macros)

#### 19.2.1. Story: Ferris’s Magic Word
Ferris got tired of having to write long repetitive commands every day. For example, every time he wants to build a vector with a few numbers, he has to write `Vec::new()` and call `push` several times. One day he found a magic spellbook that taught him how to create his **own spells**. In Rust these spells are called **Macros**! ✨📖

#### 19.2.2. What Is a Macro and How Is It Different from a Function?
| Feature | Function | Macro |
|---------|----------|-------|
| When it runs | at runtime | at compile‑time |
| Main job | perform operations and calculations | automatically generate Rust code |
| Number of inputs | fixed and known | can be variable and arbitrary |
| Mark | plain name | ends with `!` (`println!`) |

Macros are like a **smart copy‑paste factory** that write code for you before your program is built!

#### 19.2.3. The Simplest Macro with `macro_rules!`
To create a macro we use `macro_rules!`:
```rust
macro_rules! say_hello {
    () => {
        println!("Hello from the magic macro! 🦀");
    };
}

fn main() {
    say_hello!(); // at compile time this becomes println!
}
```
`()` means “if you call the macro with no arguments, replace it with the code on the right”.

#### 19.2.4. Macros with Parameters (`ident`)
We can give input to a macro. For example, take a function name and let the macro build that function:
```rust
macro_rules! create_function {
    ($name:ident) => {
        fn $name() {
            println!("Function {} was called! ✨", stringify!($name));
        }
    };
}

create_function!(foo);
create_function!(bar);

fn main() {
    foo(); // prints: Function foo was called!
    bar(); // prints: Function bar was called!
}
```
`$name:ident` means “take a valid identifier (like a variable or function name)”. `stringify!` turns the name into a string.

#### 19.2.5. Macros with a Variable Number of Arguments
This is where the real magic of macros lies: they can take **any number** of inputs! With `$($x:expr),*` we say “zero or more expressions separated by commas”:
```rust
macro_rules! sum {
    ($($x:expr),*) => {
        {
            let mut total = 0;
            $(total += $x;)* // this line repeats for each input
            total
        }
    };
}

fn main() {
    let s = sum!(1, 2, 3, 4);
    println!("Sum: {}", s); // 10
}
```
`$(...)*` means “repeat the pattern inside the parentheses as many times as there are inputs”.

#### 19.2.6. Commonly Used Macros in Rust
| Macro | Use |
|-------|-----|
| `println!(...)` | print to the terminal |
| `vec![...]` | quickly build a vector |
| `format!(...)` | build a formatted string |
| `assert!(...)` | check a condition in tests |
| `dbg!(...)` | quickly print a value for debugging |

#### 19.2.7. Exercise: The `easy_vec!` Macro
Create a macro that works exactly like `vec!`: it takes a list of values and returns a `Vec`.

💡 **Answer:**
```rust
macro_rules! easy_vec {
    ($($x:expr),* $(,)?) => {
        {
            let mut v = Vec::new();
            $(v.push($x);)*
            v
        }
    };
}

fn main() {
    let v = easy_vec![10, 20, 30];
    println!("{:?}", v); // [10, 20, 30]
}
```
💡 `$(,)?` means “it’s okay if you leave an extra comma at the end of the list”.

![[Illustration: A cartoon wizard crab (Ferris) holding a glowing spellbook labeled "macro_rules!". Floating magical symbols like "$x:expr" and "=>" transform into actual Rust code blocks. Background: cozy library with starry windows. Style: whimsical, educational children's book illustration, soft lighting, 16:9.]](../assets/images/19.2.png)

---

### 19.3. Project: Building the `repeat!` Macro

#### 19.3.1. Goal
We will build a macro that repeats a command several times. For example:
```rust
repeat!(println!("Hello! 🦀"), 3);
```
and get the output:
```
Hello! 🦀
Hello! 🦀
Hello! 🦀
```

#### 19.3.2. Implementing `repeat!`
To allow the macro to repeat **full statements** (like `let x = 5;`), we use `stmt` instead of `expr`:
```rust
macro_rules! repeat {
    ($cmd:stmt, $count:expr) => {
        for _ in 0..$count {
            $cmd;
        }
    };
}
```
Very simple! `$cmd` is the statement and `$count` is the number of repetitions. The macro turns it into a `for` loop.

#### 19.3.3. Testing the Macro
```rust
fn main() {
    repeat!(println!("Ferris is cool!"), 3);
    repeat!(let x = 5; println!("x = {}", x), 2);
}
```
The output is exactly what we wanted. See how with a few lines of code we built a custom tool? 🛠️✨

---

### 19.4. Summary and Challenge

#### 19.4.1. Concept Review
✅ `unsafe`: the part of Rust where memory safety becomes the programmer’s responsibility. Only for low‑level, essential work.  
✅ Raw pointers (`*const T`, `*mut T`): unchecked by the compiler; must be used inside `unsafe`.  
✅ Macro (`macro_rules!`): code generator at compile time. Ends with `!`.  
✅ Macro patterns: `$name:ident` (identifier), `$($x:expr),*` (list of expressions).  
✅ `$(...)*`: repeat code for each input.  
✅ **You have travelled to the deepest layers of Rust – from the `unsafe` engine to the magic of macros. A true computer wizard now knows what tools are available!** 🧙

> 🧠 **Sometimes things are hard, and that’s okay!**  
> `unsafe` and macros are among the most advanced topics in Rust. Even professional programmers rarely use `unsafe` and write complicated macros with caution. If you still feel you don’t understand everything, don’t worry – this chapter is about awareness, not mastery. The important thing is that you know how and where you can use these tools.

#### 19.4.2. Challenge: The `create_function!` Macro
Create a macro that takes a function name, a start number, and an end number. It should generate a function that prints all numbers from start to end. Use `stringify!` to show the function name.

💡 **Sample answer:**
```rust
macro_rules! create_function {
    ($name:ident, $start:expr, $end:expr) => {
        fn $name() {
            println!("Function {} is running: 👇", stringify!($name));
            for i in $start..=$end {
                println!("  number: {}", i);
            }
        }
    };
}

create_function!(count_to_five, 1, 5);

fn main() {
    count_to_five();
}
```

---

🔚 **End of Chapter 19**

Now you know how to visit the engine room when necessary and how to create your own custom spells with macros. In Chapter 20, our final adventure, we will build a small network among Ferris’s friends to send secret messages and create a space chat room! Ready for the end of this space journey? 🌌📡🦀

![[Illustration: Ferris wearing a graduation cap and safety goggles, holding a glowing "Chapter 19 Master" badge. Floating around him are an unsafe engine core, macro spell symbols, and a repeating loop arrow. Encouraging, vibrant children's book illustration, celebratory mood, 16:9.]](../assets/images/19.3.png)