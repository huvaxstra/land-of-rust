# 🦀 The Land of Rust: Ferris the Crab's Space Adventures  
## Chapter 12: The Mini-Robot Searcher (A Command-Line Project)

> 📋 *Chapter Outline:*
> - [12.1. Building a Tiny Robot (Simple grep)](#121-building-a-tiny-robot-simple-grep)
> - [12.2. Getting Command-Line Arguments](#122-getting-command-line-arguments)
> - [12.3. Reading a File](#123-reading-a-file)
> - [12.4. The Search Logic](#124-the-search-logic)
> - [12.5. Testing Our Mini-Robot](#125-testing-our-mini-robot)
> - [12.6. Making It Smarter](#126-making-it-smarter)
> - [12.7. Summary & Challenge](#127-summary--challenge)

---

## 12.1. Building a Tiny Robot (Simple grep)

### 12.1.1. The Story: Searching Ferris’s Space Diary
Ferris has a very thick space diary where he writes down all his cosmic adventures. One day, he wonders: *“How many times did I write the word ‘dinosaur’ in my diary?”* 🦕

He could flip through page by page, but that would take hours! 😴

Instead, Ferris decides to build a tiny search robot that does the work for him. The robot asks: *“What word should I search for? In which file?”* Then it quickly shows Ferris every line that contains that word. 🤖✨  

**This means you’re building your very first command-line tool – a big step toward becoming a computer wizard!** 🧙‍♂️

> 👨‍👩‍👧 **Note for Parents and Teachers**  
> This project combines concepts from earlier chapters (input, structs, error handling, testing). If your child feels confused about certain parts (like lifetimes in the `search` function), don’t worry – this is just a brief mention, and understanding it deeply isn’t required to run the program. The official Rust book has a complete implementation of this same tool:  
> [doc.rust-lang.org/book/ch12-00-an-io-project.html](https://doc.rust-lang.org/book/ch12-00-an-io-project.html)

### 12.1.2. Project Goal
Our program will do exactly this. We’ll build a command-line tool that:
1. Takes two inputs from the user: the search word + the file path.
2. Opens the file and reads its contents.
3. Finds and prints every line containing the word.

This is exactly what the famous `grep` command does in Linux and macOS. We’ll name our program `minigrep` (meaning “tiny grep”).

### 12.1.3. Creating the Project with Cargo
First, let’s create a new project:
```bash
cargo new minigrep
cd minigrep
```
Open `src/main.rs`. For simplicity, we’ll write all the code right here.

*(💡 Tip: If you want to use `edition = "2024"` in `Cargo.toml`, that’s perfectly fine – our code works with both editions.)*

**[Illustration: A friendly cartoon crab (Ferris) standing next to a small, boxy robot with a magnifying glass lens. The robot is scanning an open giant notebook with glowing search lines. Background: cozy spaceship desk with a starry window. Style: vibrant children's book illustration, soft lighting, playful tech metaphor.]**

---

## 12.2. Getting Command-Line Arguments

### 12.2.1. Introducing `std::env::args`
When you run a program from the terminal, you can add extra words after the program name. For example:
```bash
cargo run -- dinosaur poem.txt
```
Those extra words (`dinosaur poem.txt`) are called **command-line arguments**. In Rust, the `std::env` module has a function called `args` that gives us these words. It’s like handing the robot a note before we turn it on! 📝

### 12.2.2. Collecting Arguments into a `Vec`
```rust
use std::env;

fn main() {
    let args: Vec<String> = env::args().collect();
    println!("Arguments: {:?}", args);
}
```
If you run the program with the command above, the output looks something like this:
```
Arguments: ["target/debug/minigrep", "dinosaur", "poem.txt"]
```
🔹 Index 0: The program name itself (we don’t need this).  
🔹 Index 1: The search word.  
🔹 Index 2: The file path.

### 12.2.3. Building a `Config` Struct
Instead of constantly using `args[1]` and `args[2]` in our code (which gets confusing), let’s build a neat `struct` to hold our settings in one place:
```rust
struct Config {
    query: String,
    file_path: String,
}
```
`query`: The word we’re searching for. `file_path`: The file’s address.

### 12.2.4. A `build` Function for `Config`
Let’s write an associated function that takes the arguments, checks if there are enough, and builds a `Config`. If not, it returns an error:
```rust
impl Config {
    fn build(args: &[String]) -> Result<Config, &'static str> {
        if args.len() < 3 {
            return Err("Not enough arguments! You must provide a word and a file.");
        }
        let query = args[1].clone();
        let file_path = args[2].clone();
        Ok(Config { query, file_path })
    }
}
```
💡 *Why `clone()`?* Because `args` owns the strings. We don’t want to take ownership and break things. `clone()` makes a clean, independent copy. (In bigger projects there are more efficient ways, but here simplicity matters most!)

### 12.2.5. Error Handling in `main`
Now in `main`, we use `build`. If it returns an error, we print a friendly message and exit with code 1 (which signals an error):
```rust
use std::process;

fn main() {
    let args: Vec<String> = env::args().collect();

    let config = Config::build(&args).unwrap_or_else(|err| {
        eprintln!("❌ Error in arguments: {}", err);
        eprintln!("✅ Usage: cargo run -- <word> <file>");
        process::exit(1);
    });

    println!("🔍 Searching for '{}' in file '{}'", config.query, config.file_path);
}
```
📌 `eprintln!` is like `println!`, but it writes to the error output (`stderr`). This way, if you save the program’s output to a file, error messages won’t get mixed up with the data!

**[Illustration: A cartoon command-line terminal with floating speech bubbles. One bubble says "cargo run -- word file.txt". A small config card labeled "Config { query, path }" is being stamped "APPROVED". Ferris watches with a checklist. Style: clean educational vector, bright colors, clear UI metaphor.]**

---

## 12.3. Reading a File

### 12.3.1. Using `std::fs`
To work with files, we use the `std::fs` module:
```rust
use std::fs;
```

### 12.3.2. Reading File Contents
The `fs::read_to_string` function is very convenient: it opens the file, reads all the text, and converts it to a `String`:
```rust
let contents = fs::read_to_string(&config.file_path)
    .unwrap_or_else(|err| {
        eprintln!("❌ Cannot read file '{}': {}", config.file_path, err);
        process::exit(1);
    });
```

### 12.3.3. Handling File-Opening Errors
If the file doesn’t exist or we don’t have permission to read it, `unwrap_or_else` catches the error, prints a friendly message, and exits the program. This way, the user isn’t left confused! 📂🔍

---

## 12.4. The Search Logic

### 12.4.1. The `search` Function
Now let’s write a function that takes the file text and the search word, goes line by line, and returns the lines that contain the word:
```rust
fn search<'a>(query: &str, contents: &'a str) -> Vec<&'a str> {
    let mut results = Vec::new();
    for line in contents.lines() {
        if line.contains(query) {
            results.push(line);
        }
    }
    results
}
```
🔹 `.lines()` splits the text based on line breaks.  
🔹 `.contains(query)` checks if the word is in the line.  
🔹 If yes, it adds that line to `results`.

### 12.4.2. A Simple Explanation of Lifetimes in `search`
You see `'a` here. Don’t panic! This is just a safety label. It means:  
*“The lines I return are pieces of the original `contents`. So as long as `contents` is alive, this list is valid too. Don’t delete the original text while I’m still using it!”*

The compiler uses this label to make sure memory stays safe. For now, just know it’s there for safety! 🛡️

### 12.4.3. Printing Results
Now in `main`, after reading the file:
```rust
let results = search(&config.query, &contents);

if results.is_empty() {
    println!("❌ No lines containing '{}' were found.", config.query);
} else {
    println!("📋 Lines found:");
    for line in results {
        println!("  {}", line);
    }
}
```
If nothing is found, it says “Nothing found.” If something is found, it shows each line one by one! ✅

**[Illustration: A magnifying glass hovering over a long scroll of text. Highlighted lines glow with a soft yellow light while others remain dim. A tiny conveyor belt carries matching lines into a box labeled "Vec<&str>". Ferris operates the controls. Style: playful technical metaphor, warm lighting, children's book illustration.]**

---

## 12.5. Testing Our Mini-Robot

### 12.5.1. Writing a Test for `search`
Before we send our robot out into the world, let’s test it in the lab. We’ll write a unit test:
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_search_one_result() {
        let query = "dinosaur";
        let contents = "\
My name is Ferris.
Dinosaurs were very big.
I am afraid of dinosaurs.";

        assert_eq!(
            vec!["Dinosaurs were very big."],
            search(query, contents)
        );
    }
}
```
We have a sample text and check that only the line containing “dinosaur” is returned.

### 12.5.2. Running the Test
```bash
cargo test
```
You should see a green output: `test tests::test_search_one_result ... ok`. This means our robot is working correctly! 🟢

---

## 12.6. Making It Smarter

### 12.6.1. Case Sensitivity
So far, our search looks for the exact word. It finds `"dinosaur"` but not `"Dinosaurs"` or `"DINOSAUR"`. Sometimes users want a case‑insensitive search.

### 12.6.2. Reading the `CASE_INSENSITIVE` Environment Variable
Operating systems have hidden **environment variables** that act like advanced computer settings. If the user runs this before executing the program:
```bash
# Linux/macOS
export CASE_INSENSITIVE=1
# Windows (CMD)
set CASE_INSENSITIVE=1
```
The program understands it should do a case‑insensitive search. In code, we check:
```rust
use std::env;
let ignore_case = env::var("CASE_INSENSITIVE").is_ok();
```
If the variable exists, `is_ok()` returns `true`.

### 12.6.3. The `search_case_insensitive` Function
We build a similar function, but before comparing, we convert both the word and the line to lowercase:
```rust
fn search_case_insensitive<'a>(query: &str, contents: &'a str) -> Vec<&'a str> {
    let query = query.to_lowercase();
    let mut results = Vec::new();
    for line in contents.lines() {
        if line.to_lowercase().contains(&query) {
            results.push(line);
        }
    }
    results
}
```

### 12.6.4. Using the Environment Variable in `Config`
We expand `Config` to hold this setting too:
```rust
struct Config {
    query: String,
    file_path: String,
    ignore_case: bool,
}

impl Config {
    fn build(args: &[String]) -> Result<Config, &'static str> {
        if args.len() < 3 {
            return Err("Not enough arguments");
        }
        let query = args[1].clone();
        let file_path = args[2].clone();
        let ignore_case = env::var("CASE_INSENSITIVE").is_ok();
        Ok(Config { query, file_path, ignore_case })
    }
}
```
And in `main`, we decide based on it:
```rust
let results = if config.ignore_case {
    search_case_insensitive(&config.query, &contents)
} else {
    search(&config.query, &contents)
};
```

**[Illustration: A cartoon control panel with two switches: "Case-Sensitive (ON)" and "Case-Insensitive (OFF)". A glowing environment variable label "CASE_INSENSITIVE=1" flips the switch. Ferris adjusts a dial with a smile. Style: clean, educational infographic, bright colors.]**

---

## 12.7. Summary & Challenge

### 12.7.1. What You Learned
In this chapter, you discovered:
✅ How to get command-line arguments with `std::env::args`.  
✅ How to organize settings neatly with `struct Config`.  
✅ How to read a file with `std::fs::read_to_string`.  
✅ How to search text with `lines()` and `contains()`.  
✅ How to write tests with `#[cfg(test)]` and `assert_eq!`.  
✅ How to use environment variables for advanced settings.  
✅ How to manage errors cleanly with `Result` and `unwrap_or_else`.  
✅ **Building a command-line tool means you can command the computer – that’s what a real computer wizard does!** 🧙

> 🧠 **Sometimes things are hard, and that’s okay!**  
> The `minigrep` project is one of the first serious projects in learning Rust. Some parts (like lifetimes in the `search` function) might seem fuzzy at first. Don’t worry – what matters is that the program works. With time and more practice, these concepts will become clearer.

### 12.7.2. Challenge: Search for Multiple Words
Now make the program one step more professional! Let the user enter multiple words separated by `|`, and have the program find lines containing at least one of those words.

Example run:
```bash
cargo run -- "dinosaur|spaceship|star" poem.txt
```

💡 *Hint:* You can split the string with `split('|')` and then use `any()` to check if the line contains at least one of the words.

💡 *Sample Answer (main part):*
```rust
fn search_multiple<'a>(queries: &[&str], contents: &'a str) -> Vec<&'a str> {
    let mut results = Vec::new();
    for line in contents.lines() {
        if queries.iter().any(|q| line.contains(q)) {
            results.push(line);
        }
    }
    results
}
```
To use it in `main`, call it like this:
```rust
let query_list: Vec<&str> = config.query.split('|').collect();
let results = search_multiple(&query_list, &contents);
```

Now you’ve built a real, usable, tested command-line tool! You can share it with friends or even use it in your future projects. 🛠️🚀

In the next chapter, we’ll explore **Iterators and Closures** – tools that make your code cleaner, shorter, and more professional, just like a space Swiss Army knife! 🔪✨

**[Illustration: Ferris wearing a graduation cap and holding a glowing "Chapter 12 Master" badge. Around him float CLI command lines, search magnifying glasses, test checkmarks, and environment variable tags. Style: encouraging, vibrant children's book illustration, celebratory mood.]**

---

> 🔚 **End of Chapter 12**
