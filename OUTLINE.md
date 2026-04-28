# 📚 The Land of Rust – Full Chapter Outline

*20 Chapters + Teacher's Guide | Ages 9+ | Story-Driven Curriculum*

---

## 🌱 Level 1: Beginner (Ages 9–11)
*Focus: Core concepts through play, visual metaphors, and simple projects*

| Ch | Title | Key Concepts | Metaphor / Story Hook | Final Project |
|----|-------|--------------|----------------------|---------------|
| 1 | Ferris and the Lost Toolbox | Installing Rust, `cargo`, `println!`, compilation basics | Ferris unpacks his "toolbox" (Rust tools) after crash-landing | Print a welcome message: "Earth, I am here!" |
| 2 | The Missing Star Game | Variables, mutability, user input, `if/else`, loops, `match` | Ferris searches for lost stars using clues (conditional logic) | Guess-the-Number game with hints |
| 3 | The Space Chocolate Cake Recipe | Functions, parameters, return types, primitive types (`i32`, `f64`, `bool`, `char`) | Baking a cake with Ferris: ingredients = parameters, result = return value | Area calculator for Ferris's garden |
| 4 | Ferris's Borrowing Club | Ownership, moves, copying, borrowing (`&`, `&mut`), slices | Toy tractor borrowing club: who has the toy? When must it return? | `first_word` function with string slices |

---

## 🌟 Level 2: Intermediate (Ages 12–14)
*Focus: Structuring code, handling errors, and building reusable components*

| Ch | Title | Key Concepts | Metaphor / Story Hook | Final Project |
|----|-------|--------------|----------------------|---------------|
| 5 | Monster ID Cards | Structs, methods, associated functions | Creating ID cards for space monsters Ferris meets | Monster roster with display methods |
| 6 | The Smart Wardrobe | Enums, `Option`, `match`, `if let` | Ferris picks outfits based on weather (enum variants) | Weather-based clothing recommender |
| 7 | The Big City Library | Modules, files, `pub`, `use`, visibility | Organizing Ferris's knowledge in a library system | Refactor guess-the-number into modules |
| 8 | The Magic Backpack (Collections) | `Vec`, `HashMap`, `HashSet`, iteration | Ferris's backpack holds different items with labels | Interactive alien phonebook |
| 9 | When the Spaceship Breaks | `panic!`, `Result`, `?`, error propagation, `map_err` | Fixing spaceship parts that might fail (error handling) | Resilient calculator with error messages |
| 10 | The Toy Factory | Generics, traits, `impl Trait`, trait objects, `Box<dyn Trait>` | A mold (trait) that shapes different toys (types) | Shape library: calculate area/perimeter |
| 11 | Test the Self-Destruct Button! | Unit tests, `#[test]`, `assert!`, integration tests, `should_panic` | Testing Ferris's gadgets before launch (test-driven safety) | Write tests for the Monster struct |

---

## 🚀 Level 3: Advanced (Ages 14+)
*Focus: Real-world patterns, concurrency, and systems thinking*

| Ch | Title | Key Concepts | Metaphor / Story Hook | Final Project |
|----|-------|--------------|----------------------|---------------|
| 12 | Mini-robot Searcher (`minigrep`) | CLI args, file I/O, environment variables, `env_logger` | Ferris builds a search robot to find lost items | Clone of `grep`: search text in files |
| 13 | The Magic Train (Iterators & Closures) | Iterators, adapters (`map`, `filter`, `collect`), closures, `Fn` traits | A train (iterator) that transforms cargo (data) at each station | Fibonacci sequence generator with iterators |
| 14 | The Big Supermarket (Crates.io) | Using external crates, SemVer, `Cargo.lock`, publishing a crate | Ferris shops for tools in the cosmic marketplace | Build & publish a `pig_latin` crate |
| 15 | Nesting Boxes (Smart Pointers) | `Box<T>`, `Rc<T>`, `RefCell<T>`, interior mutability, `Weak` (brief) | Boxes that can hold references to other boxes (graph structures) | Simple graph with `Rc<RefCell<Node>>` |
| 16 | Ants Carrying a Leaf (Concurrency) | `thread::spawn`, `join`, channels (`mpsc`), `Mutex`, `Arc` | Ants (threads) cooperate to carry a big leaf (shared data) | Thread-safe counter incremented 1M times |
| 17 | Is Rust a Transformer? (OOP Patterns) | Composition over inheritance, traits for behavior, trait objects | Ferris designs RPG characters using flexible traits | RPG battle simulation: Warrior, Mage, Archer |
| 18 | Advanced Treasure Maps | Destructuring, match guards, `@`, `|`, nested patterns | Reading complex treasure maps with multiple conditions | Command parser for a text-based adventure game |
| 19 | Open the Engine Room! | `unsafe`, raw pointers, FFI basics, `macro_rules!` intro | Ferris accesses the spaceship's core engine (advanced power) | Custom `repeat!` macro for DRY code |
| 20 | FerrisNet – The Secret Friend Network | TCP sockets, client-server architecture, multi-threading, `Arc<Mutex<Vec>>` | Ferris builds a chat network to connect with space friends | Multi-client group chat room |

---

## 🧭 Teacher's Guide (Separate File: `teacher-guide.md`)

### Target Audience Breakdown
| Age Group | Recommended Chapters | Adult Support Level |
|-----------|---------------------|-------------------|
| 9–11 | 1–8 | High (co-reading, hands-on help) |
| 12–13 | 1–14 | Medium (guidance on complex topics) |
| 14+ | All chapters | Low (independent learning) |

### Sample 90-Minute Session Structure
1. **Warm-up (10 min)**: Review previous concept with a quick game
2. **Story Time (15 min)**: Read Ferris's adventure for the chapter
3. **Concept Exploration (25 min)**: Hands-on coding with guided examples
4. **Project Build (30 min)**: Work on chapter's final project
5. **Wrap-up (10 min)**: Share results, Q&A, preview next adventure

### Troubleshooting Common Hurdles
- 🔧 *"cargo not found"*: Step-by-step PATH setup guide with screenshots
- 🤔 *"I don't understand borrowing"*: Physical toy demonstration script
- 😰 *"The compiler error is scary"*: "Friendly Error Translator" cheat sheet
- ⏱️ *"We're running out of time"*: Optional "skip-ahead" markers per chapter

### Certificate Template
Printable completion certificate with Ferris artwork, customizable name/date.

### FAQs for Non-Programmer Adults
- "Do I need to know Rust to help my child?" → No! Guide is designed for co-learning.
- "What if we get stuck?": Community resources + debug checklist included.
- "How much time per week?" → Flexible: 1–2 sessions of 60–90 minutes.

---

> 🔄 *Outline subject to refinement based on Rust Edu feedback and pilot testing.*