# Land of Rust: Ferris the Space Crab’s Adventures  
## Chapter 18: Complex Treasure Maps (Advanced Pattern Matching)

### 📑 Chapter Index
[18.1. Difficult Puzzles: Extracting from Inside Structures](#181-difficult-puzzles-extracting-from-inside-structures)  
[18.1.1. Story: Nested Boxes](#1811-story-nested-boxes)  
[18.1.2. Destructuring Structs](#1812-destructuring-structs)  
[18.1.3. Destructuring Enums](#1813-destructuring-enums)  
[18.1.4. Destructuring Tuples](#1814-destructuring-tuples)  
[18.1.5. Destructuring in `for` Loops](#1815-destructuring-in-for-loops)  
[18.1.6. Exercise: Destructuring a Nested Struct](#1816-exercise-destructuring-a-nested-struct)  
[18.2. Negation Patterns and Conditions](#182-negation-patterns-and-conditions)  
[18.2.1. Ignoring with `_` and `..`](#1821-ignoring-with-_-and-)  
[18.2.2. Conditions in Patterns (Match Guards)](#1822-conditions-in-patterns-match-guards)  
[18.2.3. The `@` Operator for Binding](#1823-the--operator-for-binding)  
[18.2.4. `|` Patterns (OR)](#1824--patterns-or)  
[18.2.5. Exercise: Match Guard for Numbers](#1825-exercise-match-guard-for-numbers)  
[18.3. Project: Parsing Game Commands](#183-project-parsing-game-commands)  
[18.3.1. Defining the `Command` Enum](#1831-defining-the-command-enum)  
[18.3.2. The `parse_command` Function](#1832-the-parse_command-function)  
[18.3.3. Executing Commands with `match` and Guards](#1833-executing-commands-with-match-and-guards)  
[18.4. Summary and Challenge](#184-summary-and-challenge)  
[18.4.1. Concept Review](#1841-concept-review)  
[18.4.2. Challenge: Extracting from `Option<Vec<i32>>`](#1842-challenge-extracting-from-optionveci32)  

---

### 18.1. Difficult Puzzles: Extracting from Inside Structures

#### 18.1.1. Story: Nested Boxes
Ferris has found an old, dusty treasure map. 🗺️✨ But the map has a secret: the treasure is inside a box, that box is inside a chest, the chest is in a big vault, and the key to the vault is with a space bird! Ferris cannot open all those layers one by one – it would take too much time. Luckily, Ferris has a magical power: **Pattern Matching**. With one swift move, he can break through the whole structure and pull the treasure straight out of the boxes. In Rust, this is called **Destructuring**. Don’t worry – nothing is destroyed! It just means we open up a structure to reach its inner data.  
**This means you can act like a professional detective, take apart any complicated structure, and reach the treasure inside – that’s the power of a computer wizard!** 🧙‍♂️

![[Illustration: A cartoon treasure map on a wooden desk. Glowing nested boxes (small box inside medium box inside big chest) float above the map. A pair of glowing magic scissors labeled "Destructuring" cuts through the layers, revealing a shiny gold coin inside. Ferris the crab watches with excited eyes, holding a magnifying glass. Style: whimsical children's book illustration, bright, adventurous, 16:9.]](../assets/images/18.1.png)

> 👨‍👩‍👧 **Note for parents and teachers**  
> Advanced patterns are one of Rust’s most powerful features, helping children elegantly extract data from structures. If the child struggles with `@` or `_`, don’t worry – they will be used many times in later projects. The official Rust book has a whole chapter on patterns:  
> [doc.rust-lang.org/book/ch18-00-patterns.html](https://doc.rust-lang.org/book/ch18-00-patterns.html)

#### 18.1.2. Destructuring Structs
Suppose you have a `struct` called `Point` that holds the coordinates of a point. You can unpack its fields into new variables in a single line:
```rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p = Point { x: 10, y: 20 };
    
    // full syntax: field name, colon, new variable name
    let Point { x: a, y: b } = p;
    println!("a = {}, b = {}", a, b);
    
    // shorthand: if the variable name matches the field name
    let Point { x, y } = p;
    println!("x = {}, y = {}", x, y);
}
```
If you only need one field and want to ignore the rest, you can use `..`:
```rust
let Point { x, .. } = p; // takes only x, ignores y
println!("only x = {}", x);
```

#### 18.1.3. Destructuring Enums
In Chapter 6 you learned that an `enum` can have different variants. `match` is the best tool for opening these variants. Let’s look at a space‑message `enum`:
```rust
enum Message {
    Quit,                       // no data
    Move { x: i32, y: i32 },    // an anonymous struct
    Write(String),              // a string
    ChangeColor(u8, u8, u8),    // a tuple
}

fn process(msg: Message) {
    match msg {
        Message::Quit => println!("👋 Quit program"),
        Message::Move { x, y } => println!("🚀 Move to ({}, {})", x, y),
        Message::Write(text) => println!("📝 Writing: {}", text),
        Message::ChangeColor(r, g, b) => {
            println!("🎨 Change colour to ({}, {}, {})", r, g, b);
        }
    }
}
```
Look how easily we extracted the nested data! `match` understands the shape of each variant and gives you exactly what is inside.

#### 18.1.4. Destructuring Tuples
Tuples are also very easy to destructure:
```rust
let t = (1, 2, 3);
let (x, y, z) = t;
println!("x={}, y={}, z={}", x, y, z);
```
You can even destructure a tuple directly in a function’s parameters:
```rust
fn print_coordinates(&(x, y): &(i32, i32)) {
    println!("Coordinates: ({}, {})", x, y);
}
```

#### 18.1.5. Destructuring in `for` Loops
This feature is very useful in `for` loops, especially when working with `HashMap`:
```rust
let points = vec![(0, 0), (1, 2), (3, 4)];
for (x, y) in points {
    println!("Next point: ({}, {})", x, y);
}
```
Each iteration pulls a tuple from the list, and `(x, y)` neatly assigns its values. It’s not magic, just Rust being smart! 😉

#### 18.1.6. Exercise: Destructuring a Nested Struct
Define a `struct` called `Person` with fields `name: String` and `address: Address`. `Address` itself is a `struct` with fields `city: String` and `zip: u32`. Create an instance of `Person` and **in one destructuring line** extract both `name` and `city` directly, then print them.

💡 **Sample answer:**
```rust
struct Address {
    city: String,
    zip: u32,
}

struct Person {
    name: String,
    address: Address,
}

fn main() {
    let person = Person {
        name: String::from("Ferris"),
        address: Address {
            city: String::from("Crab City"),
            zip: 12345,
        },
    };
    
    // nested destructuring: take name directly, and from address only take city
    let Person { name, address: Address { city, .. } } = person;
    
    println!("{} lives in the city of {}.", name, city);
}
```
💡 Notice: `address: Address { city, .. }` means “go into the `address` field, treat it as an `Address`, unpack it, but only keep `city`, ignore the rest.”

![[Illustration: A 3D puzzle cube being taken apart layer by layer. Each layer reveals a smaller cube inside, finally revealing a tiny star. Ferris stands on a stack of books, wearing a detective hat and holding a magnifying glass. Style: educational vector, bright colors, clear visual metaphor, 16:9.]](../assets/images/18.2.png)

---

### 18.2. Negation Patterns and Conditions

Sometimes during pattern matching, we want to ignore certain things or match only when an extra condition holds. This is where the magic of `match` becomes complete! 🪄

#### 18.2.1. Ignoring with `_` and `..`
🔹 `_` (underscore): acts like a trash can for patterns – anything placed there is ignored.  
🔹 `..` : ignores the rest of the fields in a `struct` or the rest of the elements in a tuple/array.

```rust
struct Point3D { x: i32, y: i32, z: i32 }
let p = Point3D { x: 1, y: 2, z: 3 };
let Point3D { x, .. } = p; // only x matters, y and z are ignored

let numbers = (1, 2, 3, 4, 5);
let (first, .., last) = numbers; // only the first and last
println!("first: {}, last: {}", first, last);
```

#### 18.2.2. Conditions in Patterns (Match Guards)
Sometimes a pattern alone is not enough. For example, you want to say “if the number is even” or “if the string length is greater than 5”. We do this with a **Match Guard**: an `if` that comes right after the pattern.
```rust
let num = Some(4);

match num {
    Some(x) if x % 2 == 0 => println!("{} is an even number!", x),
    Some(x) => println!("{} is an odd number.", x),
    None => println!("There is no number."),
}
```
⚠️ Order matters! If you write `Some(x)` without the `if` first, that arm will always match and the guard will never be checked.

#### 18.2.3. The `@` Operator for Binding
The `@` sign is a super tool: while checking a pattern, it also stores the whole matched value in a variable.
For example, we want to know if a number is in the range 1..=10, and at the same time keep the number itself:
```rust
let x = 5;

match x {
    num @ 1..=10 => println!("{} is in the range 1 to 10.", num),
    _ => println!("{} is out of range.", x),
}
```
Here `num` becomes the value of `x`, but only if it falls inside the range `1..=10`.

#### 18.2.4. `|` Patterns (OR)
If several patterns should execute the same code, you don’t have to write separate arms. Combine them with `|` (vertical bar):
```rust
let x = 2;

match x {
    1 | 2 => println!("One of the numbers 1 or 2."),
    3 => println!("Number 3."),
    _ => println!("Something else."),
}
```

#### 18.2.5. Exercise: Match Guard for Numbers
Write a program that reads a number from the user. Using `match` and a guard, determine:
- If the number is between 1 and 10 → print “small”.
- If the number is between 11 and 20 → print “medium”.
- Otherwise → print “big or out of range”.

💡 **Sample answer:**
```rust
use std::io;

fn main() {
    let mut input = String::new();
    println!("Enter a number:");
    io::stdin().read_line(&mut input).unwrap();
    let num: i32 = input.trim().parse().unwrap();

    match num {
        n if (1..=10).contains(&n) => println!("Number {} is small. 👶", n),
        n if (11..=20).contains(&n) => println!("Number {} is medium. 👦", n),
        _ => println!("Number {} is big or not in range. 🌳", num),
    }
}
```
💡 `(1..=10).contains(&n)` is a clean way to check membership in a range!

---

### 18.3. Project: Parsing Game Commands

Now it’s time to test all these tools in a real project! 🎮 Let’s build a simple command system for a text‑based game. The user types commands like `/go north` or `/attack dragon 50`, and the program understands and executes them.

#### 18.3.1. Defining the `Command` Enum
First we define an `enum` for the possible command types:
```rust
enum Command {
    Go { direction: String },
    Attack { target: String, power: u32 },
    Quit,
}
```

#### 18.3.2. The `parse_command` Function
We write a function that splits the input string (by whitespace) and returns a `Command`. If the input is empty or has the wrong format, we treat it as `Quit`.
```rust
fn parse_command(input: &str) -> Command {
    let parts: Vec<&str> = input.trim().split_whitespace().collect();
    
    // if the user didn't enter anything
    if parts.is_empty() {
        return Command::Quit;
    }
    
    // if the user typed "/go north"
    if parts[0] == "/go" && parts.len() >= 2 {
        Command::Go {
            direction: parts[1].to_string(),
        }
    } 
    // if the user typed "/attack dragon 50"
    else if parts[0] == "/attack" && parts.len() >= 3 {
        let power = parts[2].parse().unwrap_or(10); // if not a number, default to 10
        Command::Attack {
            target: parts[1].to_string(),
            power,
        }
    } 
    // otherwise, "/quit" or anything else
    else {
        Command::Quit
    }
}
```

#### 18.3.3. Executing Commands with `match` and Guards
Now in `main` we run a loop to read commands and execute them. We use `match` with a guard to show a special message for very powerful attacks:
```rust
use std::io;
use std::io::Write; // for flush

fn main() {
    println!("🎮 Welcome to Ferris’s text game!");
    loop {
        print!("\nType your command (/go, /attack, /quit): ");
        io::stdout().flush().unwrap(); // make sure the message prints immediately
        
        let mut input = String::new();
        io::stdin().read_line(&mut input).unwrap();
        let cmd = parse_command(&input);

        match cmd {
            Command::Go { direction } => {
                println!("🚀 Ferris moves towards {}.", direction);
            }
            Command::Attack { target, power } if power > 30 => {
                println!("💥 Devastating attack! {} is obliterated with {} power!", target, power);
            }
            Command::Attack { target, power } => {
                println!("⚔️ Attacked {} with {} power. (Still alive!)", target, power);
            }
            Command::Quit => {
                println!("👋 Goodbye! The game is over.");
                break;
            }
        }
    }
}
```
Look how clean it became! No more nested `if/else`. `match` opens everything like a treasure map. 🗝️

![[Illustration: A retro computer terminal screen showing text commands: "/go north", "/attack dragon 50", "/quit". Next to the screen, a cartoon joystick with buttons labeled "Match", "Guard", "Enum". Ferris sits at the keyboard wearing a gaming headset, smiling confidently. Style: cozy gaming setup, vibrant, children's book illustration, 16:9.]](../assets/images/18.3.png)

---

### 18.4. Summary and Challenge

#### 18.4.1. Concept Review
In this chapter you learned:
✅ **Destructuring**: extracting fields from `struct`s, `enum`s, and `tuple`s using patterns.  
✅ `_` and `..`: ignoring parts of a pattern when you don’t need them.  
✅ **Match Guards**: adding an `if` condition to a `match` arm.  
✅ `@` Binding: storing a matched value in a variable while checking the pattern.  
✅ `|` (OR): combining several patterns in one arm to avoid repetition.  
✅ **These tools turn you into a data detective – a true computer wizard!** 🧙

> 🧠 **Sometimes things are hard, and that’s okay!**  
> Nested destructuring and match guards might feel a bit complex at first. Don’t worry – the more you use them in your code, the more natural they become. Even professional programmers sometimes try several times to write a complicated pattern. The important thing is that Rust always tells you where you made a mistake.

#### 18.4.2. Challenge: Extracting from `Option<Vec<i32>>`
Write a function called `sum_first_two` that takes an `Option<Vec<i32>>` as input and:
- If it is `Some` and the vector has at least 3 elements, return the sum of the first two elements as `Some(i32)`.
- If it is `Some` but has fewer than 3 elements, return `None`.
- If it is `None`, return `None`.

💡 **Hint:** You can use a nested `match` or a `match guard`.

💡 **Sample answer:**
```rust
fn sum_first_two(opt: Option<Vec<i32>>) -> Option<i32> {
    match opt {
        Some(vec) if vec.len() >= 3 => Some(vec[0] + vec[1]),
        _ => None, // covers both Some with short length and None
    }
}

fn main() {
    let v1 = Some(vec![10, 20, 30, 40]);
    let v2 = Some(vec![5, 15]);
    let v3 = None;

    println!("{:?}", sum_first_two(v1)); // Some(30)
    println!("{:?}", sum_first_two(v2)); // None
    println!("{:?}", sum_first_two(v3)); // None
}
```

---

🔚 **End of Chapter 18**

Now you are a pattern‑matching master! You can unpack the most complex data structures like a pro. 🧩✨  
In the next chapter we’ll visit the engine room of Rust and explore `unsafe` and macros – tools used only by professional, adventurous heroes! Are you ready for some (safe) black magic? 🌙🔧

![[Illustration: Ferris wearing a graduation cap and holding a glowing "Chapter 18 Master" badge. Floating around him are nested puzzle boxes, match guard shields, and a joystick controller. Background: a starry night sky with a subtle map overlay. Encouraging, vibrant children's book style, 16:9.]](../assets/images/18.4.png)
