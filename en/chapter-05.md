# 🦀 The Land of Rust: Ferris the Crab's Space Adventures
## Chapter 5: Monster ID Cards (Structs)

> 📋 *Chapter Outline:*
> - [5.1. What Does My Monster Look Like?](#51-what-does-my-monster-look-like)
> - [5.2. The Monster Application Form (Defining a Struct)](#52-the-monster-application-form-defining-a-struct)
> - [5.3. Introducing a New Monster (Creating Instances)](#53-introducing-a-new-monster-creating-instances)
> - [5.4. Things Monsters Can Do (Methods)](#54-things-monsters-can-do-methods)
> - [5.5. Project: The Monster Roster](#55-project-the-monster-roster)
> - [5.6. Summary & Challenge](#56-summary--challenge)

---

## 5.1. What Does My Monster Look Like?

### 5.1.1. The Story: Ferris's Monster Notebook
During his space travels, Ferris has met dozens of strange and wonderful creatures. Some are giant, some are tiny and cute. Ferris decided to create a notebook to keep track of each monster: What's its name? What color is it? How many legs does it have? How strong is it?

This information works exactly like an ID card for each creature. In programming, when we want to keep related information together and organized, we use a fantastic tool called a **`struct`** (short for *structure*).

### 5.1.2. The Problem: Too Many Separate Variables
If we tried to store a monster's information without a `struct`, we'd need a bunch of separate variables:
```rust
let name = String::from("Dodo");
let color = String::from("green");
let legs = 4;
let power = 100;
```
For one monster, it's fine. But what if we have ten monsters? We'd end up with messy names like `name2`, `color3`, and it would be impossible to pass all that information to a function as one neat package.

### 5.1.3. Introducing `struct` as an ID Card Template
A `struct` lets us group several pieces of data together under one name. Think of it like a blank ID card template. First, we design the template (deciding what fields it will have), and then we fill out real cards for different monsters.

**[Illustration: A magical notebook open on a wooden desk. The left page shows messy scattered variables tied together with tangled string. The right page displays a clean, glowing ID card template with labeled slots: "Name", "Color", "Legs", "Power". Ferris stands proudly pointing at the organized page. Style: vibrant children's book illustration, educational metaphor, soft lighting, 16:9.]**

---

## 5.2. The Monster Application Form (Defining a Struct)

### 5.2.1. Writing a Simple Struct
We start with the keyword `struct`, give it a name, and list its fields inside `{}`:
```rust
struct Monster {
    name: String,
    color: String,
    legs: u8,
    power: u32,
}
```
This code says: *"I'm creating a new blueprint called `Monster`. Every monster made from this blueprint will have four parts: a name (`String`), a color (`String`), leg count (`u8`, a small positive number), and power (`u32`)."*

### 5.2.2. Naming Rules: `PascalCase` vs `snake_case`
In Rust, we follow a neat naming tradition:
🔹 **Struct names** use `PascalCase`: Each word starts with a capital letter, no spaces. Examples: `Monster`, `SpaceShip`, `StudentGrade`.
🔹 **Field names** use `snake_case`: All lowercase, words separated by underscores. Examples: `name`, `legs_count`, `fuel_amount`.

### 5.2.3. Fields and Their Types
Each field has a name and a type. You can use any type you've learned so far: `i32`, `f64`, `bool`, `char`, `String`, or even other `struct`s! For example, you could make a `Coordinates` struct and put it inside `Monster`:
```rust
struct Coordinates {
    x: f64,
    y: f64,
}

struct Monster {
    name: String,
    position: Coordinates,
    // other fields...
}
```

### 5.2.4. Exercise: Define a Spaceship Struct
Create a `struct` named `SpaceShip` with three fields:
- `fuel` of type `u32` (remaining fuel)
- `passenger_count` of type `u8` (number of passengers)
- `model` of type `String` (spaceship model)

💡 **Sample Answer**:
```rust
struct SpaceShip {
    fuel: u32,
    passenger_count: u8,
    model: String,
}
```

**[Illustration: An educational infographic showing a Rust struct definition as a blueprint sheet. Fields are highlighted with colorful tags matching their data types (String=blue, u8=green, u32=orange). Ferris holds a ruler and pencil, drawing the blueprint. Style: clean, modern educational cartoon, bright colors, 16:9.]**

---

## 5.3. Introducing a New Monster (Creating Instances)

### 5.3.1. Making a Real Monster (Instance)
Now that we have the `Monster` blueprint, let's create an actual monster. We write the struct name, open `{}`, and give each field a value:
```rust
let monster1 = Monster {
    name: String::from("Dodo"),
    color: String::from("green"),
    legs: 4,
    power: 100,
};
```
Now `monster1` is a real monster holding Dodo's information!

### 5.3.2. Accessing Fields with a Dot (`.`)
To read a field, we use the dot operator, just like visiting a specific room in a house:
```rust
println!("Monster name: {}", monster1.name);
println!("Power level: {}", monster1.power);
```

### 5.3.3. Changing Fields (With `mut`)
If we want to change a field later (like training the monster to get stronger), we must create the instance with `mut`:
```rust
let mut monster2 = Monster {
    name: String::from("Bombi"),
    color: String::from("red"),
    legs: 2,
    power: 50,
};

monster2.power = 75;  // Now Bombi's power is 75!
```

### 5.3.4. Shortcut: Field Init Shorthand
If you already have variables with the exact same names as the struct fields, Rust lets you skip writing `name: name`:
```rust
let name = String::from("Dodo");
let color = String::from("green");
let legs = 4;
let power = 100;

let monster = Monster {
    name,   // means name: name
    color,  // means color: color
    legs,   // means legs: legs
    power,  // means power: power
};
```
This keeps your code short and tidy! 🧹✨

### 5.3.5. Building a New Monster from an Old One (`..` Syntax)
Sometimes you want to create a monster that's almost identical to another, but with one difference. Instead of rewriting all fields, use `..`:
```rust
let monster2 = Monster {
    name: String::from("Bombi"),
    ..monster1   // copy the rest from monster1
};
```
⚠️ **Important Note**: This moves ownership for `String` fields! Because `String` doesn't implement `Copy`, `monster1.name` now belongs to `monster2`. You can't use `monster1.name` after this line. But numbers like `legs` and `power` *are* `Copy`, so they get copied safely. 
Remember: `..` is convenient, but always keep Chapter 4's ownership rules in mind!

**[Illustration: Split scene: Left shows a crab holding a "monster blueprint" copying data to a new card using a ".." stamp. Right shows a friendly warning sign: "String fields move ownership!". Ferris explains with a helpful gesture. Style: playful technical metaphor, children's book illustration, clear visual cues, 16:9.]**

---

## 5.4. Things Monsters Can Do (Methods)

### 5.4.1. Function vs Method
A **function** is a standalone block of code (like `add` from Chapter 3).
A **method** is a function that belongs to a specific `struct`. Methods are called with a dot (`.`) on an instance, and their first parameter always points to the instance itself (usually `&self`). Think of it as saying *"Monster, roar!"* instead of *"Roar at the monster!"*

### 5.4.2. Writing Your First Method with `impl`
To attach methods to a struct, we use an `impl` (implementation) block:
```rust
impl Monster {
    fn roar(&self) {
        println!("{} roooooaaar!", self.name);
    }
}
```
Now we can make any monster roar:
```rust
let dodo = Monster { /* ... */ };
dodo.roar();  // Prints: "Dodo roooooaaar!"
```

### 5.4.3. The `&self` Parameter
`&self` is an immutable reference to the current instance. It means the method can **read** fields but not change them. We have three main options:
🔹 `&self` : Read-only (most common)
🔹 `&mut self` : Read + modify (requires `mut` instance)
🔹 `self` : Take ownership (destroys the instance after use – rare)

### 5.4.4. Methods with Extra Parameters
Methods can take extra parameters besides `&self`:
```rust
impl Monster {
    fn attack(&self, target: &str) {
        println!("{} attacked {} with {} power!", self.name, target, self.power);
    }
}
```
Usage: `dodo.attack("Bill");`

### 5.4.5. Methods with Return Values
Methods can return values just like regular functions:
```rust
impl Monster {
    fn power_level(&self) -> u32 {
        self.power
    }
}
```

### 5.4.6. Modifying Methods (`&mut self`)
If a method needs to change the instance's data, it must use `&mut self`, and the instance must be `mut`:
```rust
impl Monster {
    fn heal(&mut self, amount: u32) {
        self.power += amount;
        println!("{} powered up to {}!", self.name, self.power);
    }
}
```
Usage: `bombi.heal(20);`

### 5.4.7. Associated Functions (Like `new`)
Sometimes we want a function related to the struct that doesn't need an instance. The most famous example is `new`, which builds a fresh monster. We call these with `::` (double colon):
```rust
impl Monster {
    fn new(name: String, color: String, legs: u8, power: u32) -> Monster {
        Monster { name, color, legs, power }
    }
}
```
Usage:
```rust
let dodo = Monster::new(
    String::from("Dodo"),
    String::from("green"),
    4,
    100,
);
```
This feels like a "monster factory"! 🏭

**[Illustration: Cartoon scene showing a "Method Factory" conveyor belt. Crabs input raw monster parts, a machine labeled "impl Monster" adds behaviors (roar, attack, heal) via &self/&mut self tags, and finished monsters roll out with speech bubbles. Ferris operates a control panel. Style: dynamic, educational, bright colors, 16:9.]**

---

## 5.5. Project: The Monster Roster

Now let's build a small program that stores a list of monsters and performs actions on them.

### 5.5.1. Creating a `Vec` of Monsters
First, we'll use a `Vec` (vector) to store monsters. A `Vec` is like a magical backpack that automatically grows when you add items. (We'll explore `Vec` deeply in Chapter 8, but for now, just know we add items with `.push()`.)
```rust
let mut monster_list = Vec::new();

monster_list.push(Monster::new(
    String::from("Dodo"), String::from("green"), 4, 100,
));
monster_list.push(Monster::new(
    String::from("Bombi"), String::from("red"), 2, 75,
));
monster_list.push(Monster::new(
    String::from("Zarzar"), String::from("yellow"), 6, 120,
));
```

### 5.5.2. Looping to Make Everyone Roar
We want every monster in the list to roar. Rust has a simple loop called `for` that automatically visits each item one by one:
```rust
for monster in &monster_list {
    monster.roar();
}
```
💡 **Why `&monster_list`?** The `&` means we're *borrowing* the list, not taking ownership. Just like the borrowing cards from Chapter 4!

### 5.5.3. Finding the Strongest Monster
Let's write a function that returns the monster with the highest `power`:
```rust
fn strongest(monsters: &Vec<Monster>) -> &Monster {
    let mut strongest = &monsters[0];
    for monster in monsters {
        if monster.power > strongest.power {
            strongest = monster;
        }
    }
    strongest
}
```
Usage in `main`:
```rust
let champ = strongest(&monster_list);
println!("Strongest monster: {} with power {}", champ.name, champ.power);
```

### 5.5.4. Exercise: `is_stronger_than` Method
Add a method to `Monster` called `is_stronger_than` that takes another `&Monster` and returns `true` if the current monster is stronger.

💡 **Sample Answer**:
```rust
impl Monster {
    fn is_stronger_than(&self, other: &Monster) -> bool {
        self.power > other.power
    }
}
```
Usage:
```rust
if dodo.is_stronger_than(&bombi) {
    println!("Dodo is stronger than Bombi!");
}
```

**[Illustration: A cozy notebook open to a "Monster Roster" page. Each entry shows a mini ID card with a cartoon monster sketch and stats. A golden trophy icon highlights the strongest monster. Ferris sits on the desk stamping "Approved" with a smile. Style: warm, inviting children's book illustration, detailed UI metaphor, 16:9.]**

---

## 5.6. Summary & Challenge

### 5.6.1. What You Learned
In this chapter, you discovered:
✅ `struct` is a template for grouping related data.
✅ Instances are created with `let x = StructName { fields };`
✅ Access fields with the dot operator (`.`).
✅ Methods are defined in `impl` blocks and use `self`, `&self`, or `&mut self`.
✅ Associated functions (like `new`) are called with `::`.
✅ The `..` syntax copies remaining fields (watch out for ownership moves!).
✅ The `for` loop is a simple way to visit each item in a list.

### 5.6.2. Challenge: Student Struct & Grades
Create a `struct` named `Student` with `name: String` and `grade: f64`. Write a method `passed(&self) -> bool` that returns `true` if `grade >= 10.0`. Then, create a `Vec` of students and print only those who passed.

💡 **Sample Answer**:
```rust
struct Student {
    name: String,
    grade: f64,
}

impl Student {
    fn new(name: String, grade: f64) -> Student {
        Student { name, grade }
    }

    fn passed(&self) -> bool {
        self.grade >= 10.0
    }
}

fn main() {
    let students = vec![
        Student::new(String::from("Sara"), 18.5),
        Student::new(String::from("Reza"), 9.0),
        Student::new(String::from("Maryam"), 14.0),
    ];

    for student in &students {
        if student.passed() {
            println!("{} passed with grade {}", student.name, student.grade);
        } else {
            println!("{} needs more practice.", student.name);
        }
    }
}
```

Now you know how to organize related data into `struct`s and give them behaviors with methods! In the next chapter, we'll explore `enum` and learn how to handle different states (like weather, game modes, or traffic lights) in a clean, safe way. 🌈✨

**[Illustration: Ferris wearing a graduation cap, holding a glowing "Chapter 5 Complete" badge. Floating around him are mini structs, impl blocks, and &self tags turning into a neat organized library. Encouraging, bright lighting, children's book style.]**

---

> 🔚 **End of Chapter 5**

---
