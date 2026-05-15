# Land of Rust: Ferris the Space Crab’s Adventures  
## Chapter 15: The Secret of Nested Boxes (Smart Pointers)

### 📑 Chapter Index
[15.1. The Gift Box (Box<T>)](#151-the-gift-box-boxt)  
[15.1.1. Story: A Big Present in a Small Box](#1511-story-a-big-present-in-a-small-box)  
[15.1.2. What is Box<T>?](#1512-what-is-boxt)  
[15.1.3. Simple Use of Box](#1513-simple-use-of-box)  
[15.1.4. Use Case: Recursive Structures (Linked List)](#1514-use-case-recursive-structures-linked-list)  
[15.1.5. Exercise: Box for a Trait Object](#1515-exercise-box-for-a-trait-object)  
[15.2. The Library’s Shared Book (Rc<T>)](#152-the-librarys-shared-book-rct)  
[15.2.1. Story: A Book Several People Read at the Same Time](#1521-story-a-book-several-people-read-at-the-same-time)  
[15.2.2. What is Rc<T>?](#1522-what-is-rct)  
[15.2.3. Creating Rc and Cloning](#1523-creating-rc-and-cloning)  
[15.2.4. Counting References](#1524-counting-references)  
[15.2.5. Limitations: Read‑Only and Single‑Threaded](#1525-limitations-read-only-and-single-threaded)  
[15.2.6. Exercise: Rc with Multiple Owners](#1526-exercise-rc-with-multiple-owners)  
[15.2.7. The Memory Leak Problem and the Weak Solution](#1527-the-memory-leak-problem-and-the-weak-solution)  
[15.3. The Group Notebook (RefCell<T>)](#153-the-group-notebook-refcellt)  
[15.3.1. Story: A Notebook Everyone Can Write In](#1531-story-a-notebook-everyone-can-write-in)  
[15.3.2. What is RefCell<T>?](#1532-what-is-refcellt)  
[15.3.3. borrow and borrow_mut](#1533-borrow-and-borrow_mut)  
[15.3.4. Breaking the Rules at Runtime](#1534-breaking-the-rules-at-runtime)  
[15.3.5. Combining Rc and RefCell](#1535-combining-rc-and-refcell)  
[15.3.6. Exercise: Rc<RefCell<i32>>](#1536-exercise-rcrefcelli32)  
[15.4. Project: A Simple Graph System](#154-project-a-simple-graph-system)  
[15.4.1. Defining a Node](#1541-defining-a-node)  
[15.4.2. Building a Graph with Rc<RefCell<Node>>](#1542-building-a-graph-with-rcrefcellnode)  
[15.4.3. Adding an Edge](#1543-adding-an-edge)  
[15.4.4. Simple Traversal and Cycle Warning](#1544-simple-traversal-and-cycle-warning)  
[15.5. Summary and Challenge](#155-summary-and-challenge)  
[15.5.1. Concept Review](#1551-concept-review)  
[15.5.2. Challenge: Doubly‑Linked List with Rc<RefCell<Node>> and an Introduction to Weak](#1552-challenge-doubly-linked-list-with-rcrefcellnode-and-an-introduction-to-weak)

---

### 15.1. The Gift Box (Box<T>)

#### 15.1.1. Story: A Big Present in a Small Box
Ferris has a very large, heavy gift that is hard to carry around. 🎁 But he finds a small, light cardboard box. He puts the gift inside the box, and now he only needs to carry that light box!  
Inside a computer there are also two storage places:  
🔹 **Stack (the workbench):** very fast, but has limited space. It only holds small things.  
🔹 **Heap (the big warehouse):** plenty of space, but getting in and out is a little slower.  
When our data is large, we send it to the Heap and keep only a small address (like a barcode) on the Stack. `Box<T>` is exactly that cardboard box that does this for us! 📦✨

#### 15.1.2. What is Box<T>?
`Box<T>` is a smart pointer that takes data of type `T` and stores it in the Heap. When the `Box` goes out of scope (for example, when we leave a function), the data inside the Heap is automatically cleaned up.  
It has three main uses:  
1. Storing large data without cluttering the Stack.  
2. Building recursive structures (like linked lists).  
3. Holding Trait Objects (which we’ll see later).

#### 15.1.3. Simple Use of Box
```rust
fn main() {
    let b = Box::new(5); // the number 5 goes to the Heap, its address stays on the Stack
    println!("Value inside the box: {}", b); // we use it like a normal number
}
```

#### 15.1.4. Use Case: Recursive Structures (Linked List)
Suppose we want to build a train where each wagon connects to the next. In Rust we cannot write a `struct` that directly contains itself (because its size would be infinite!). But with `Box` (which has a fixed size) there is no problem:
```rust
enum List {
    Cons(i32, Box<List>), // a number + a pointer to the rest of the train
    Nil,                  // last wagon (empty)
}

use List::{Cons, Nil};

fn main() {
    let train = Cons(1, Box::new(Cons(2, Box::new(Cons(3, Box::new(Nil))))));
}
```

#### 15.1.5. Exercise: Box for a Trait Object
Create a trait called `Draw` with a method `draw(&self)`. Write two structs `Circle` and `Square` that implement it. Then create a `Vec<Box<dyn Draw>>`, put the shapes in it, and call `draw` on each one.

💡 **Answer:**
```rust
trait Draw { fn draw(&self); }

struct Circle;
impl Draw for Circle { fn draw(&self) { println!("○ Circle drawn!"); } }

struct Square;
impl Draw for Square { fn draw(&self) { println!("□ Square drawn!"); } }

fn main() {
    let shapes: Vec<Box<dyn Draw>> = vec![Box::new(Circle), Box::new(Square)];
    for shape in shapes { shape.draw(); }
}
```

![[Illustration: A friendly cartoon crab (Ferris) holding a small glowing gift box labeled "Box<T>". Inside the box, a larger, heavy golden item sits safely. A conveyor belt moves the box to a large warehouse labeled "Heap", while a small barcode tag stays on a desk labeled "Stack". Style: vibrant children's book illustration, educational metaphor, soft lighting, 16:9.]](../assets/images/15.1.png)

---

### 15.2. The Library’s Shared Book (Rc<T>)

#### 15.2.1. Story: A Book Several People Read at the Same Time
In Ferris’s library there is a very famous book. Several people want to borrow it at the same time. In normal Rust each value has only one owner, but with `Rc<T>` (short for Reference Counted) we can have multiple owners at the same time. `Rc` counts how many people are holding the book. When the last person returns the book, it automatically goes back to the shelf (the memory is freed). 📚🔢

#### 15.2.2. What is Rc<T>?
`Rc<T>` is a smart pointer with reference counting. Every time you create a new `Rc` from it, a hidden counter increases by one. When an `Rc` goes out of scope, the counter decreases. When it reaches zero, the data is freed.  
To use it we must bring it into scope: `use std::rc::Rc;`

#### 15.2.3. Creating Rc and Cloning
```rust
let a = Rc::new(5);      // counter = 1
let b = Rc::clone(&a);   // counter = 2 (notice: the data is not copied, only the counter increases)
let c = Rc::clone(&a);   // counter = 3
```

#### 15.2.4. Counting References
We can see how many borrows exist:
```rust
let book = Rc::new(String::from("Magic Book"));
println!("Number of borrowers: {}", Rc::strong_count(&book)); // 1
let reader = Rc::clone(&book);
println!("Number of borrowers: {}", Rc::strong_count(&book)); // 2
```

#### 15.2.5. Limitations: Read‑Only and Single‑Threaded
⚠️ `Rc` only allows you to **read** the data (immutable borrow). If you want to change it, you must combine it with `RefCell`.  
⚠️ Also, `Rc` is only safe for single‑threaded programs. For multi‑threaded programs we use its cousin `Arc`.

#### 15.2.6. Exercise: Rc with Multiple Owners
Create a `struct` called `Book` with a `title` field. Create three `Rc<Book>` that all point to the same book. Print the title and show the reference count.

💡 **Answer:**
```rust
use std::rc::Rc;
struct Book { title: String }

fn main() {
    let book = Rc::new(Book { title: String::from("Ferris’s Adventures") });
    let r1 = Rc::clone(&book);
    let r2 = Rc::clone(&book);
    println!("Title: {}", book.title);
    println!("Readers: {}", Rc::strong_count(&book)); // 3
}
```

#### 15.2.7. The Memory Leak Problem and the Weak Solution
Up to here everything is fine, but there is a trap! If we create a **cycle** with `Rc` (for example, node A points to B and B points back to A), the counters will never drop to zero. That means the memory of those nodes **leaks** until the program ends. 😟  
To solve this problem, Rust has another smart pointer called `Weak<T>`. `Weak` is like `Rc` but it does not increase the strong count (it has its own weak count). To turn an `Rc` into a `Weak` we use `Rc::downgrade`.  
In projects like bidirectional graphs or doubly‑linked lists, we use `Weak` for one of the directions to break the cycle. Don’t worry – we’ll mention it in the challenge at the end of the chapter and see more of it in later advanced chapters.

![[Illustration: A cartoon library desk with a single glowing book. Three children hold transparent "Rc" cards connected by dotted lines to the book. A small digital counter on the book shows "3". Ferris stands nearby holding a clipboard, smiling. Style: clean educational vector, bright colors, clear metaphor, 16:9.]](../assets/images/15.2.png)

---

### 15.3. The Group Notebook (RefCell<T>)

#### 15.3.1. Story: A Notebook Everyone Can Write In
The children in the library have a shared notebook. Everyone can read it, but when someone wants to write in it, they must ensure nobody else is reading or writing at that same moment. In Rust this rule is usually checked at compile time, but `RefCell<T>` moves that check to **runtime**. If someone breaks the rule, the program politely stops with a `panic!`. 📓✍️

#### 15.3.2. What is RefCell<T>?
`RefCell<T>` is a smart pointer that allows you to mutably borrow what appears to be an immutable piece of data, as long as at runtime there is only one writer at a time.  
To use it: `use std::cell::RefCell;`

#### 15.3.3. borrow and borrow_mut
🔹 `.borrow()` → returns a normal reference (`&T`) (read‑only).  
🔹 `.borrow_mut()` → returns a mutable reference (`&mut T`) (read+write).
```rust
let x = RefCell::new(5);
{
    let mut y = x.borrow_mut(); // write lock opened
    *y += 10;
} // lock closed
println!("Value: {}", x.borrow()); // 15
```

#### 15.3.4. Breaking the Rules at Runtime
If you try to have two `borrow_mut` at the same time, the program stops:
```rust
let x = RefCell::new(5);
let a = x.borrow_mut();
let b = x.borrow_mut(); // ❌ panic! two writers at the same time
```
The compiler won’t give an error here, so you have to be careful yourself!

#### 15.3.5. Combining Rc and RefCell
Real magic happens when we combine the two: `Rc<RefCell<T>>`. Now multiple owners can see the same data and each of them (one at a time) can change it:
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::ops::AddAssign;

let shared = Rc::new(RefCell::new(0));
Rc::clone(&shared).borrow_mut().add_assign(5); // +5
Rc::clone(&shared).borrow_mut().add_assign(3); // +3
println!("Final: {}", shared.borrow()); // 8
```

#### 15.3.6. Exercise: Rc<RefCell<i32>>
Create a number `10` of type `Rc<RefCell<i32>>`. Write two functions `add_two` and `multiply_by_three` that each work on that same number. Finally print the value.

💡 **Answer:**
```rust
fn add_two(num: &Rc<RefCell<i32>>) { *num.borrow_mut() += 2; }
fn multiply_by_three(num: &Rc<RefCell<i32>>) { *num.borrow_mut() *= 3; }

fn main() {
    let n = Rc::new(RefCell::new(10));
    add_two(&n);
    multiply_by_three(&n);
    println!("Result: {}", n.borrow()); // 36
}
```

![[Illustration: A cartoon notebook on a table with a glowing lock icon. One hand holds a blue key labeled "borrow", another hand waits with a golden key labeled "borrow_mut". A traffic light shows green for reading, red for simultaneous writing. Ferris explains with a pointer. Style: playful educational illustration, clear visual rules, bright, 16:9.]](../assets/images/15.3.png)

---

### 15.4. Project: A Simple Graph System

Now let’s put all these boxes together and build a space map! A graph is a set of nodes that can be connected to each other. 🌌🔗

#### 15.4.1. Defining a Node
```rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug)]
struct Node {
    name: String,
    neighbors: Vec<Rc<RefCell<Node>>>,
}
```

#### 15.4.2. Building a Graph with Rc<RefCell<Node>>
```rust
fn main() {
    let a = Rc::new(RefCell::new(Node { name: "Planet A".into(), neighbors: vec![] }));
    let b = Rc::new(RefCell::new(Node { name: "Planet B".into(), neighbors: vec![] }));
    let c = Rc::new(RefCell::new(Node { name: "Planet C".into(), neighbors: vec![] }));

    // A connects to B and C
    a.borrow_mut().neighbors.push(Rc::clone(&b));
    a.borrow_mut().neighbors.push(Rc::clone(&c));

    // B also connects back to A (two‑way)
    b.borrow_mut().neighbors.push(Rc::clone(&a));

    println!("A’s neighbors: {:?}", a.borrow().neighbors.iter().map(|n| &n.borrow().name).collect::<Vec<_>>());
}
```

#### 15.4.3. Adding an Edge
We can write a helper function to make connecting nodes easier:
```rust
fn add_edge(from: &Rc<RefCell<Node>>, to: &Rc<RefCell<Node>>) {
    from.borrow_mut().neighbors.push(Rc::clone(to));
}
```

#### 15.4.4. Simple Traversal and Cycle Warning
⚠️ **Important warning:** If the graph contains a cycle, a simple traversal might run forever! For safe traversal we must keep a `HashSet` of already‑visited nodes.  
⚠️ **Memory leak:** If the graph has a cycle and all connections use `Rc`, the memory of those nodes will never be freed (the same problem as in section 15.2.7). To build professional graphs we should use `Weak` for some of the edges. Don’t worry – this chapter is only an introduction to these ideas.

![[Illustration: A star map with glowing planet nodes labeled A, B, C. Glowing lines connect them bidirectionally. Small floating boxes labeled "Rc" and "RefCell" hover near each node, showing data flow. Ferris points to a connection with a space pen. Style: cozy sci-fi workspace, educational vector, soft glow, 16:9.]](../assets/images/15.4.png)

---

### 15.5. Summary and Challenge

#### 15.5.1. Concept Review
| Tool | Main Use | Important Limitation |
|------|----------|----------------------|
| `Box<T>` | Sending data to the Heap, recursive structures | Has only one owner |
| `Rc<T>` | Multiple owners (single‑threaded) | Read‑only; risk of leaks if cycles exist |
| `Weak<T>` | Breaking `Rc` cycles | Must be upgraded with `upgrade` to access |
| `RefCell<T>` | Changing data through an immutable reference | Borrow rules checked at runtime |
| `Rc<RefCell<T>>` | Multiple owners + (turn‑based) mutability | Panic on rule violation + risk of cyclic leaks |

#### 15.5.2. Challenge: Doubly‑Linked List with Rc<RefCell<Node>> and an Introduction to Weak
Build a doubly‑linked list. Each node should have `prev` and `next` fields. Use `Option<Rc<RefCell<Node>>>`.  

💡 **Professional tip:** In the real world, if you use `Rc` for both `prev` and `next`, you will create a memory leak. The standard solution is to use `Weak<RefCell<Node>>` for the `prev` field. The final shape would be:

```rust
use std::rc::{Rc, Weak};
use std::cell::RefCell;

struct Node {
    value: i32,
    next: Option<Rc<RefCell<Node>>>,
    prev: Option<Weak<RefCell<Node>>>,
}
```

For now, it’s okay to practice with only `Rc` – but know that for real‑world code you should use `Weak`. If you feel adventurous, you can replace it right now and access the data with `upgrade`. 🧠

![[Illustration: Ferris wearing a graduation cap and safety goggles, holding a glowing "Chapter 15 Master" badge. Floating around him are a gift box (Box), a shared book (Rc), a notebook with a lock (RefCell), and a small star map graph. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/15.5.png)