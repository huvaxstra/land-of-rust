# Land of Rust: Ferris the Space Crab’s Adventures  
## Chapter 13: The Magic Train and the Transformation Factory (Iterators & Closures)

### 📑 Chapter Index
[13.1. The Cargo Train (Iterator)](#131-the-cargo-train-iterator)  
[13.1.1. Story: The Train of Stone Wagons](#1311-story-the-train-of-stone-wagons)  
[13.1.2. What Is an Iterator?](#1312-what-is-an-iterator)  
[13.1.3. Getting an Iterator from a Collection](#1313-getting-an-iterator-from-a-collection)  
[13.1.4. The `next` Method](#1314-the-next-method)  
[13.1.5. The `for` Loop and Iterator](#1315-the-for-loop-and-iterator)  
[13.1.6. Exercise: Traversing with `while let`](#1316-exercise-traversing-with-while-let)  
[13.2. Machines Along the Track (Adapter Methods)](#132-machines-along-the-track-adapter-methods)  
[13.2.1. `map`: Transforming Each Element](#1321-map-transforming-each-element)  
[13.2.2. `filter`: Selecting Based on a Condition](#1322-filter-selecting-based-on-a-condition)  
[13.2.3. Chaining](#1323-chaining)  
[13.2.4. `collect`: Gathering Results](#1324-collect-gathering-results)  
[13.2.5. Other Useful Methods (`fold`, `any`, `all`, `sum`)](#1325-other-useful-methods-fold-any-all-sum)  
[13.2.6. Exercise: Squared Even Numbers](#1326-exercise-squared-even-numbers)  
[13.3. The Spy Backpack (Closures)](#133-the-spy-backpack-closures)  
[13.3.1. Story: Ferris’s Secret Tool](#1331-story-ferriss-secret-tool)  
[13.3.2. Defining a Closure](#1332-defining-a-closure)  
[13.3.3. Capturing Variables from the Environment](#1333-capturing-variables-from-the-environment)  
[13.3.4. Capture Types (`Fn`, `FnMut`, `FnOnce`)](#1334-capture-types-fn-fnmut-fnonce)  
[13.3.5. Moving Ownership with `move`](#1335-moving-ownership-with-move)  
[13.3.6. Exercise: Multiplier Closure](#1336-exercise-multiplier-closure)  
[13.4. Combining Iterator and Closure](#134-combining-iterator-and-closure)  
[13.4.1. `map` with a Closure](#1341-map-with-a-closure)  
[13.4.2. `filter` with a Closure](#1342-filter-with-a-closure)  
[13.4.3. Example: Reading Lines from stdin and Converting to Numbers](#1343-example-reading-lines-from-stdin-and-converting-to-numbers)  
[13.4.4. `filter_map` for Combining Two Jobs](#1344-filter_map-for-combining-two-jobs)  
[13.5. Project: Processing a Log File](#135-project-processing-a-log-file)  
[13.5.1. Structure of Log Lines](#1351-structure-of-log-lines)  
[13.5.2. Reading a File with Iterator](#1352-reading-a-file-with-iterator)  
[13.5.3. Filtering ERROR Lines](#1353-filtering-error-lines)  
[13.5.4. Counting Errors with a HashMap](#1354-counting-errors-with-a-hashmap)  
[13.6. Summary and Challenge](#136-summary-and-challenge)  
[13.6.1. Concept Review](#1361-concept-review)  
[13.6.2. Challenge: Implementing Iterator for Fibonacci](#1362-challenge-implementing-iterator-for-fibonacci)  

---

### 13.1. The Cargo Train (Iterator)

#### 13.1.1. Story: The Train of Stone Wagons
Ferris has a big cargo train whose wagons are filled with sparkling stones from different planets. 🚂💎 He doesn’t want to dump all the stones at once and make a mess on the ground. He prefers the train to move slowly and open only one wagon at a time, delivering one stone at a time. This is called **Iteration**.  
In programming, when we work with lists or collections, we often need to look at each member one by one. The tool that does this for us in an orderly way is called an **Iterator**.  
**Here we learn how to traverse data without writing long loops – a big step toward professional coding!** 🧙‍♂️

> 👨‍👩‍👧 **Note for parents and teachers**  
> Iterators and Closures are powerful Rust features that enable clean, efficient code. This chapter might be challenging for some children – don’t worry, they will be used many times in later projects. The official Rust book has a whole chapter on Iterators:  
> [doc.rust-lang.org/book/ch13-00-functional-features.html](https://doc.rust-lang.org/book/ch13-00-functional-features.html)

#### 13.1.2. What Is an Iterator?
An Iterator is a smart being that knows how to hand out the members of a collection one by one, in order, and only when asked. In Rust, the `Iterator` trait is standard; its most important tool is the `next` method:
```rust
trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
}
```
🔹 Every time you call `next`, it gives you the next member inside `Some(member)`.  
🔹 When there are no more members, it returns `None`.  
💡 **Golden tip:** Iterators are **lazy**! They don’t do any work until you ask for the next item or collect the results. That means they don’t waste memory or speed! ⏱️

#### 13.1.3. Getting an Iterator from a Collection
To get an Iterator from a vector or array, you have three main ways:

| Method | Output type | Simple explanation |
|--------|-------------|--------------------|
| `.iter()` | `&T` | Only **looks** (immutable borrow). The collection stays untouched. |
| `.iter_mut()` | `&mut T` | Looks and **allows modification**. |
| `.into_iter()` | `T` | Takes **ownership**. After it finishes, you can’t use the collection anymore. |

```rust
let v = vec![10, 20, 30];

let iter1 = v.iter();       // only looks
let iter2 = v.iter_mut();   // can modify
let iter3 = v.into_iter();  // takes ownership (v cannot be used after this line)
```

#### 13.1.4. The `next` Method
You can manually call `next` to see how it works:
```rust
let v = vec!["apple", "banana", "orange"];
let mut iter = v.iter(); // must be mutable because the internal position changes

assert_eq!(iter.next(), Some(&"apple"));
assert_eq!(iter.next(), Some(&"banana"));
assert_eq!(iter.next(), Some(&"orange"));
assert_eq!(iter.next(), None); // nothing left!
```

#### 13.1.5. The `for` Loop and Iterator
The good news is that you don’t have to deal with `next` yourself! The `for` loop in Rust automatically creates an Iterator behind the scenes and continues until `None` is returned:
```rust
let names = vec!["Ferris", "Bill", "Luna"];
for name in &names {   // &names is exactly the same as names.iter()
    println!("Hello {}!", name);
}
```
⚠️ If you write `for name in names` (without `&`), the loop takes ownership of `names`, and you cannot use it after the loop.

#### 13.1.6. Exercise: Traversing with `while let`
Using `while let` and `next()`, traverse the vector `["a", "b", "c"]` and print each element.

💡 **Answer:**
```rust
fn main() {
    let v = vec!["a", "b", "c"];
    let mut iter = v.iter();
    
    while let Some(item) = iter.next() {
        println!("{}", item);
    }
}
```
`while let` means: “As long as `next` returns `Some`, run the code. When it returns `None`, stop automatically.” Very clean! ✨

![[Illustration: A friendly cartoon crab (Ferris) standing on a platform next to a colorful train. Each train car has a glowing gem inside. A conveyor arm lifts one gem at a time as the train moves slowly. Background: starry sky with a control panel showing "next() → Some(gem)". Style: vibrant children's book illustration, playful tech metaphor, soft lighting, 16:9.]](../assets/images/13.1.png)

---

### 13.2. Machines Along the Track (Adapter Methods)

#### 13.2.1. `map`: Transforming Each Element
On the train track there are machines that take stones, change their shape or colour, and send them to the next wagon. In Rust, these are called **Adapters**. The most famous one is `map`. It takes a Closure and applies it to each element:
```rust
let numbers = vec![1, 2, 3];
let doubled: Vec<_> = numbers.iter().map(|x| x * 2).collect();
println!("{:?}", doubled); // [2, 4, 6]
```
⚠️ **Note:** `map` by itself does nothing! It just creates a new Iterator that says: “When I am asked, I will perform this transformation.”

#### 13.2.2. `filter`: Selecting Based on a Condition
There’s also a machine that only lets stones pass if they satisfy a certain condition. If the condition is `true`, the stone passes; if `false`, it falls off the track. To make working with references easier, we use `.copied()`:
```rust
let numbers = vec![1, 2, 3, 4, 5];
let evens: Vec<i32> = numbers.iter().copied().filter(|&x| x % 2 == 0).collect();
println!("{:?}", evens); // [2, 4]
```
`.copied()` turns `&i32` into actual `i32` values, so we don’t have to deal with `|&&x|`.

#### 13.2.3. Chaining
The beauty of Iterators is that you can chain machines one after another:
```rust
let numbers = vec![1, 2, 3, 4, 5];
let result: Vec<_> = numbers.iter()
    .copied()
    .filter(|&x| x % 2 == 0)   // first keep only evens
    .map(|x| x * 10)           // then multiply by 10
    .collect();                // finally collect them
println!("{:?}", result); // [20, 40]
```
This chain does **no computation** until it hits `.collect()` or `.sum()`. Rust is smart enough to optimize the whole pipeline! 🧠⚡

#### 13.2.4. `collect`: Gathering Results
`collect` is the final station. It takes an Iterator and gathers all the results into a new Collection (like `Vec` or `HashMap`). You usually need to specify the type: `Vec<_>` or `::<Vec<i32>>`.

#### 13.2.5. Other Useful Methods
| Method | Use | Example |
|--------|-----|---------|
| `sum()` | Sum of numbers | `numbers.iter().sum::<i32>()` |
| `fold(init, \|acc, x\| ...)` | General accumulator | `fold(0, \|acc, x\| acc + x)` |
| `any(\|&x\| ...)` | At least one satisfies the condition | `any(\|&x\| x > 10)` |
| `all(\|&x\| ...)` | All satisfy the condition | `all(\|&x\| x > 0)` |

#### 13.2.6. Exercise: Squared Even Numbers
Create a vector of numbers from 1 to 10. Using `filter` and `map`, select only the even numbers, compute their squares, and collect them into a new vector.

💡 **Answer:**
```rust
fn main() {
    let result: Vec<i32> = (1..=10)
        .filter(|&x| x % 2 == 0)
        .map(|x| x * x)
        .collect();
    println!("{:?}", result); // [4, 16, 36, 64, 100]
}
```
`(1..=10)` is a Range that already implements Iterator – no need for `vec!`!

![[Illustration: A cartoon factory conveyor belt with labeled machines: "filter", "map", "collect". Glowing cubes travel through, changing shape and color at each station. Ferris operates a control panel with a big green "Run" button. Style: educational vector, bright, clean, 16:9.]](../assets/images/13.2.png)

---

### 13.3. The Spy Backpack (Closures)

#### 13.3.1. Story: Ferris’s Secret Tool
Ferris has a magical backpack that can store a secret operation. For example, he tells it: “Whatever number you get, multiply it by 3.” Later, whenever Ferris wants, the backpack performs that operation. The real magic is that the backpack can **remember things from the surrounding environment**. In Rust, this tool is called a **Closure**. 🎒✨

#### 13.3.2. Defining a Closure
The syntax is very simple: `|parameters| { body }`. If the body is only one line, you can omit the curly braces `{}`:
```rust
let add_one = |x| x + 1;
println!("{}", add_one(5)); // 6

let multiply = |a, b| a * b;
println!("{}", multiply(4, 5)); // 20
```
The types of parameters and return value are usually inferred by the compiler.

#### 13.3.3. Capturing Variables from the Environment
A Closure can use variables that are defined outside of it:
```rust
let factor = 3;
let multiply_by_factor = |x| x * factor; // captures `factor` from the environment
println!("{}", multiply_by_factor(10)); // 30
```
But how does the Closure behave with these variables? There are three possibilities, chosen automatically by the compiler:

#### 13.3.4. Capture Types (`Fn`, `FnMut`, `FnOnce`)
| Type | Behavior | Example |
|------|----------|---------|
| `Fn` | Only **reads** (immutable borrow `&`). Can be called many times. | `|x| x + factor` |
| `FnMut` | Can **modify** (mutable borrow `&mut`). Called multiple times. | `|| { count += 1; count }` |
| `FnOnce` | Takes **ownership** and consumes it. Can be called only **once**. | `|| println!("{}", s)` when `s` is not copied. |

`FnMut` example:
```rust
let mut count = 0;
let mut increment = || {
    count += 1;
    count
};
println!("{}", increment()); // 1
println!("{}", increment()); // 2
```

#### 13.3.5. Moving Ownership with `move`
If you put the keyword `move` before the Closure, you tell it: “Please transfer ownership of the captured variables into the Closure.” This is useful when you want to send the Closure to another thread:
```rust
let s = String::from("Hello space!");
let consume = move || {
    println!("{}", s);
};
consume();
// println!("{}", s); // ❌ Error! ownership moved to `consume`
```

#### 13.3.6. Exercise: Multiplier Closure
Write a function called `make_multiplier` that takes a number `factor` and returns a Closure. The Closure should multiply any number given to it by `factor`. Use `move`.

💡 **Answer:**
```rust
fn make_multiplier(factor: i32) -> impl Fn(i32) -> i32 {
    move |x| x * factor
}

fn main() {
    let double = make_multiplier(2);
    let triple = make_multiplier(3);
    println!("{}", double(5));  // 10
    println!("{}", triple(5));  // 15
}
```

![[Illustration: A cartoon crab wearing a futuristic backpack with glowing memory chips. Around the crab float variables like "factor = 3" and "x" being pulled into the backpack. A "move" tag is stamped on the backpack. Style: playful sci-fi educational, bright colors, 16:9.]](../assets/images/13.3.png)

---

### 13.4. Combining Iterator and Closure

#### 13.4.1. `map` with a Closure
Adapters like `map` and `filter` take Closures as input:
```rust
let names = vec!["Ferris", "Bill"];
let greetings: Vec<_> = names.iter()
    .map(|name| format!("Hello {}!", name))
    .collect();
println!("{:?}", greetings); // ["Hello Ferris!", "Hello Bill!"]
```

#### 13.4.2. `filter` with a Closure
```rust
let numbers = vec![5, 15, 25, 8];
let big_numbers: Vec<_> = numbers.iter()
    .copied()
    .filter(|&x| x > 10)
    .collect();
println!("{:?}", big_numbers); // [15, 25]
```

#### 13.4.3. Example: Reading Lines from stdin and Converting to Numbers
Suppose the user enters several numbers, one per line, and we want to compute their sum:
```rust
use std::io::{self, BufRead};

fn main() {
    let stdin = io::stdin();
    let sum: i32 = stdin.lock().lines()
        .map(|line| line.unwrap().trim().parse::<i32>().unwrap())
        .sum();
    println!("Sum: {}", sum);
}
```
Here `stdin.lock().lines()` gives an Iterator over lines. `map` takes each line, trims it, and parses it into a number. Finally `sum()` adds them all up.

#### 13.4.4. `filter_map` for Combining Two Jobs
Sometimes you want to **transform** and **filter** at the same time. `filter_map` takes a Closure that returns an `Option<T>`. If it returns `Some`, keep it; if `None`, discard it:
```rust
let strings = vec!["3", "seven", "8", "10"];
let numbers: Vec<i32> = strings.iter()
    .filter_map(|s| s.parse().ok()) // if parsing fails, returns None and it’s dropped
    .collect();
println!("{:?}", numbers); // [3, 8, 10]
```
`.ok()` is a helper method that turns a `Result` into an `Option`. Very handy for cleaning up data! 🧼

![[Illustration: A cartoon sorting machine with a "filter_map" label. As items pass through, some are converted and drop into a "Collected" box while invalid items slide into a "Rejected" bin. Ferris watches the process. Style: educational, playful, bright colors, 16:9.]](../assets/images/13.4.png)

---

### 13.5. Project: Processing a Log File

Now it’s time to put it all together in a real project. Suppose you have a file `log.txt` that records system status:
```text
INFO: System initialized
ERROR: Disk is full
WARNING: Memory running low
ERROR: Network connection lost
INFO: Task finished
```
We want to find the lines that contain `ERROR` and see how many times each error occurs.

#### 13.5.1. Structure of Log Lines
Each line starts with a label like `ERROR:`. We only care about real errors.

#### 13.5.2. Reading a File with Iterator
```rust
use std::fs::File;
use std::io::{BufRead, BufReader};

fn main() {
    let file = File::open("log.txt").expect("log.txt not found");
    let reader = BufReader::new(file);
    // ... more code
}
```

#### 13.5.3. Filtering ERROR Lines
```rust
let error_lines: Vec<String> = reader.lines()
    .filter_map(|line| line.ok()) // if a line read fails, ignore it
    .filter(|line| line.starts_with("ERROR"))
    .collect();

println!("Found errors:");
for line in &error_lines {
    println!("  {}", line);
}
```

#### 13.5.4. Counting Errors with a HashMap
Now let’s see how many times each error message appears:
```rust
use std::collections::HashMap;

let mut counts = HashMap::new();
for line in reader.lines().filter_map(|l| l.ok()) {
    if let Some(msg) = line.strip_prefix("ERROR: ") {
        *counts.entry(msg.to_string()).or_insert(0) += 1;
    }
}

println!("\n📊 Error statistics:");
for (msg, count) in &counts {
    println!("  - {} : {} times", msg, count);
}
```
`strip_prefix` returns the rest of the line only if it starts with `"ERROR: "`. Then we use `entry` and `or_insert` to count occurrences. The code is clean, fast, and nice! ⚡

![[Illustration: A cartoon control desk with a scrolling screen of log lines. A glowing filter machine catches only "ERROR" tags and drops them into a counting jar. Ferris adjusts a dial labeled "filter_map". Style: cozy tech workspace, educational vector, warm lighting, 16:9.]](../assets/images/13.5.png)

---

### 13.6. Summary and Challenge

#### 13.6.1. Concept Review
In this chapter you learned:  
✅ **Iterator**: an object for step‑by‑step traversal of collections. Core method: `next`.  
✅ **`.iter()` / `.iter_mut()` / `.into_iter()`**: ways to get an Iterator with different access levels.  
✅ **Adapters**: `map` (transform), `filter` (select), `collect` (gather), `fold`/`sum`/`any`/`all`. All of them are **lazy**.  
✅ **Closure**: an anonymous function that captures environment variables. Syntax: `|x| x * 2`.  
✅ **Closure types**: `Fn` (read‑only), `FnMut` (modify), `FnOnce` (consume).  
✅ **`move`**: transfer ownership of captured variables into the Closure.  
✅ **`filter_map`**: clever combination of filtering and transformation.  
✅ **These tools allow you to write short, fast, human‑readable code – like a real wizard!** 🧙

> 🧠 **Sometimes things are hard, and that’s okay!**  
> Closures and chained Iterators might feel confusing at first. Even professional programmers sometimes try several times to build a complex chain. Don’t worry – with practice, these tools will become natural and writing beautiful code will become a joy.

#### 13.6.2. Challenge: Implementing Iterator for Fibonacci
Create a `struct` called `Fibonacci` that implements the `Iterator` trait. Each time `next` is called, it should return the next number in the Fibonacci sequence (0, 1, 1, 2, 3, 5, 8, …). Then use `.take(10)` to print the first ten numbers.

💡 **Sample answer:**
```rust
struct Fibonacci {
    current: u64,
    next: u64,
}

impl Fibonacci {
    fn new() -> Self {
        Fibonacci { current: 0, next: 1 }
    }
}

impl Iterator for Fibonacci {
    type Item = u64;

    fn next(&mut self) -> Option<Self::Item> {
        let new_next = self.current + self.next;
        let result = self.current;
        self.current = self.next;
        self.next = new_next;
        Some(result)
    }
}

fn main() {
    let fib = Fibonacci::new();
    for num in fib.take(10) {
        println!("{}", num);
    }
}
```
`take(10)` is another Adapter that returns only the first 10 elements of an Iterator. The combination of `struct + Trait + Adapter` is where Rust truly shines! 🌟

Now you know how to write cleaner, shorter, and more professional code using Iterators and Closures. In the next chapter we’ll visit the **big Rust supermarket (Crates.io)** and learn how to use ready‑made libraries to build even more powerful programs. 📦🚀