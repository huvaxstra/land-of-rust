# Land of Rust: Ferris the Space Crab’s Adventures  
## Chapter 17: Is Rust a Transformer Robot? (Object‑Oriented Programming, Rust Style)

### 📑 Chapter Index
[17.1. Traditional Robots (Inheritance)](#171-traditional-robots-inheritance)  
[17.1.1. Story: Robot Father and Robot Son](#1711-story-robot-father-and-robot-son)  
[17.1.2. Inheritance in Other Languages (e.g., Java)](#1712-inheritance-in-other-languages-eg-java)  
[17.1.3. Problems with Inheritance](#1713-problems-with-inheritance)  
[17.2. The Rust Way (Composition & Traits)](#172-the-rust-way-composition--traits)  
[17.2.1. Composition Instead of Inheritance](#1721-composition-instead-of-inheritance)  
[17.2.2. Sharing Behaviour with Traits](#1722-sharing-behaviour-with-traits)  
[17.2.3. How Rust Differs from Traditional Inheritance](#1723-how-rust-differs-from-traditional-inheritance)  
[17.2.4. Exercise: The `Sound` Trait and Implementing It for Several Types](#1724-exercise-the-sound-trait-and-implementing-it-for-several-types)  
[17.3. Project: Simulating a Simple Game](#173-project-simulating-a-simple-game)  
[17.3.1. Defining the `Attack` Trait](#1731-defining-the-attack-trait)  
[17.3.2. Defining the `Health` Struct](#1732-defining-the-health-struct)  
[17.3.3. Defining the `Warrior`, `Mage`, `Archer` Structs](#1733-defining-the-warrior-mage-archer-structs)  
[17.3.4. Implementing `Attack` for Each](#1734-implementing-attack-for-each)  
[17.3.5. Using Trait Objects (`Box<dyn Attack>`)](#1735-using-trait-objects-boxdyn-attack)  
[17.4. Summary and Challenge](#174-summary-and-challenge)  
[17.4.1. Concept Review](#1741-concept-review)  
[17.4.2. Challenge: The `Movable` Trait](#1742-challenge-the-movable-trait)

---

### 17.1. Traditional Robots (Inheritance)

#### 17.1.1. Story: Robot Father and Robot Son
In many toy factories, when they want to build a new robot, they first create a “father robot” that knows basic actions like walking and talking. Then they say: “The son robot knows all those things as well – it just also has wings!” This way, the child inherits all the father’s features. In programming this is called **Inheritance**. 🤖👨‍👦

#### 17.1.2. Inheritance in Other Languages (e.g., Java)
In languages like Java or C++, this is very common:
```java
// hypothetical Java example
class Robot {
    void walk() { /* walking */ }
}

class FlyingRobot extends Robot {
    void fly() { /* flying */ }
}
```
Now `FlyingRobot` has both `walk` (because it inherited from its parent) and `fly`. At first glance it looks great, but…

#### 17.1.3. Problems with Inheritance
Inheritance has several big problems, and Rust deliberately avoids them:
🔸 **Rigid hierarchy:** If later we want a robot that both flies and swims, we would need to inherit from two parents, which causes confusion (the diamond problem!).  
🔸 **Unwanted inheritance:** If a “Penguin” inherits from “Bird”, it also gets the `fly` method, even though penguins cannot fly!  
🔸 **Fragility:** If the engineer makes a small change to the father robot, the son robot’s code might suddenly break.

Rust says: “Instead of a rigid hierarchy, let’s work with Lego blocks (Composition) and skill certificates (Traits)!” 🧩✨  
**This approach means that instead of blind copying, you can combine behaviours like pieces from a toolbox – that’s what a computer wizard does.** 🧙‍♂️

![[Illustration: A split cartoon comparison. Left side: a rigid, tangled family tree of robots labeled "Inheritance (Messy)". Right side: neat Lego blocks labeled "Composition" being snapped together. Ferris the crab points happily at the Lego side. Style: educational vector illustration, bright colors, clear visual metaphor, 16:9.]](../assets/images/17.1.png)

---

### 17.2. The Rust Way (Composition & Traits)

#### 17.2.1. Composition Instead of Inheritance
In Rust, instead of saying “A combat robot **is a kind of** robot”, we say “A combat robot **has** an engine, a sword, and a shield.” This is called **Composition**:
```rust
struct Engine;      // engine
struct Sword;       // sword
struct Shield;      // shield

struct CombatRobot {
    engine: Engine,
    weapon: Sword,
    shield: Shield,
}
```
If later we want a flying robot, we simply add a `Wing` component. There is no need to change a whole hierarchy. Composition is like building toys with Lego – complete freedom! 🧱

#### 17.2.2. Sharing Behaviour with Traits
But what if several different robots need to perform a common action? For example, all of them should be able to sound an alarm? That’s where **Traits** come in. A trait is like a skill certificate that says: “This robot knows how to sound an alarm.”
```rust
trait MakeSound {
    fn make_sound(&self);
}

struct Dog;
impl MakeSound for Dog {
    fn make_sound(&self) { println!("Woof! Woof!"); }
}

struct Car;
impl MakeSound for Car {
    fn make_sound(&self) { println!("Beep beep!"); }
}
```
Now each of them makes a sound in its own way, but both have the `MakeSound` certificate! 🏅

#### 17.2.3. How Rust Differs from Traditional Inheritance
🔹 In Rust, you can implement as many traits as you want for a single type.  
🔹 There is no mandatory hierarchy.  
🔹 It is always clear what capability each piece has, instead of inheriting a large, confusing bundle.

#### 17.2.4. Exercise: The `Sound` Trait and Implementing It for Several Types
Define a trait called `Sound` with a method `make_sound(&self)`. Implement it for `Cat`, `Cow`, and `Phone`. Then put them in a `Vec<Box<dyn Sound>>` and make them all make their sounds.

💡 **Sample answer:**
```rust
trait Sound { fn make_sound(&self); }

struct Cat; impl Sound for Cat { fn make_sound(&self) { println!("Meow! 🐱"); } }
struct Cow; impl Sound for Cow { fn make_sound(&self) { println!("Moooo! 🐮"); } }
struct Phone; impl Sound for Phone { fn make_sound(&self) { println!("Ring ring! 📱"); } }

fn main() {
    let things: Vec<Box<dyn Sound>> = vec![
        Box::new(Cat),
        Box::new(Cow),
        Box::new(Phone),
    ];
    for thing in things { thing.make_sound(); }
}
```

![[Illustration: A cartoon quality control desk. A friendly robot inspector stamps glowing badges labeled "Sound", "Fly", "Swim" onto different cute characters (cat, cow, phone). Ferris stands beside holding a checklist, smiling. Style: clean educational cartoon, bright colors, clear visual metaphor, 16:9.]](../assets/images/17.2.png)

---

### 17.3. Project: Simulating a Simple Game

Now let’s test all this in a small role‑playing game! 🎮⚔️

#### 17.3.1. Defining the `Attack` Trait
First we create a certificate that says “anything that has this can attack”:
```rust
trait Attack {
    fn attack(&self, target: &mut Health);
}
```

#### 17.3.2. Defining the `Health` Struct
A simple structure for health (`Health`) that holds an `hp` number and can take damage:
```rust
#[derive(Debug)]
struct Health { hp: i32 }

impl Health {
    fn new(hp: i32) -> Self { Health { hp } }
    
    fn take_damage(&mut self, damage: i32) {
        self.hp -= damage;
        if self.hp < 0 { self.hp = 0; }
    }
    
    fn is_alive(&self) -> bool { self.hp > 0 }
}
```

#### 17.3.3. Defining the `Warrior`, `Mage`, `Archer` Structs
We create three different heroes:
```rust
struct Warrior { power: i32 }
struct Mage { mana: i32 }
struct Archer { arrows: i32 }
```

#### 17.3.4. Implementing `Attack` for Each
Each one attacks in its own style:
```rust
impl Attack for Warrior {
    fn attack(&self, target: &mut Health) {
        println!("⚔️ Warrior strikes with {} power!", self.power);
        target.take_damage(self.power);
    }
}

impl Attack for Mage {
    fn attack(&self, target: &mut Health) {
        let damage = self.mana / 2;
        println!("🔮 Mage casts a spell for {} damage!", damage);
        target.take_damage(damage);
    }
}

impl Attack for Archer {
    fn attack(&self, target: &mut Health) {
        let damage = self.arrows;
        println!("🏹 Archer shoots {} arrows!", damage);
        target.take_damage(damage);
    }
}
```

#### 17.3.5. Using Trait Objects (`Box<dyn Attack>`)
Now we want to have an army of different heroes and attack an enemy. Because the sizes of `Warrior`, `Mage`, and `Archer` are different, we cannot put them directly into a single array. The solution? Use a **Trait Object** and `Box`:
```rust
fn main() {
    let mut enemy = Health::new(80); // enemy with 80 HP

    let heroes: Vec<Box<dyn Attack>> = vec![
        Box::new(Warrior { power: 25 }),
        Box::new(Mage { mana: 40 }),
        Box::new(Archer { arrows: 15 }),
    ];

    for hero in heroes {
        hero.attack(&mut enemy);
        println!("Enemy status: {:?}", enemy);
        if !enemy.is_alive() {
            println!("💀 Enemy defeated!");
            break;
        }
    }
}
```
📌 **Important note:** `dyn Attack` means “in this box you can put anything that implements the `Attack` trait”. `Box` moves it to the heap so its size no longer matters. This way we can keep different types in one list and loop over them! 🎉

![[Illustration: Cartoon RPG battle scene. Three heroes (Warrior, Mage, Archer) stand on one side, each holding a glowing "Box<dyn Attack>" badge. On the other side, a cartoon monster has a health bar showing 80 → 55 → 35. Ferris acts as a referee holding a flag. Style: vibrant, dynamic children's book illustration, 16:9.]](../assets/images/17.3.png)

---

### 17.4. Summary and Challenge

#### 17.4.1. Concept Review
✅ Rust does not have class‑based inheritance.  
✅ Instead, it uses **Composition** for data and **Traits** for behaviour.  
✅ `Box<dyn Trait>` allows us to store different types that share a common trait together in one collection.  
✅ This approach makes programs more flexible, safer, and cleaner than traditional inheritance.

> 🧠 **Sometimes things are hard, and that’s okay!**  
> Understanding the difference between composition and inheritance can feel a bit abstract at first. Even experienced developers sometimes debate which approach is better. The important thing is that Rust gives you freedom without forcing you into rigid hierarchies. With practice on small projects, this concept will become clear.

#### 17.4.2. Challenge: The `Movable` Trait
Define a trait called `Movable` with a method `move_forward(&self)`. Implement this trait for three structs: `Bicycle`, `Car`, and `Boat` (e.g., a bicycle spins its wheels, a car starts its engine, a boat rows its oars). Then write a function `start_journey` that takes a slice of `&dyn Movable` and makes each one move forward.

💡 **Sample answer:**
```rust
trait Movable { fn move_forward(&self); }

struct Bicycle; impl Movable for Bicycle { fn move_forward(&self) { println!("🚲 Wheels are spinning..."); } }
struct Car; impl Movable for Car { fn move_forward(&self) { println!("🚗 Engine started, let's go!"); } }
struct Boat; impl Movable for Boat { fn move_forward(&self) { println!("⛵ Oars dip into the water..."); } }

fn start_journey(things: &[&dyn Movable]) {
    for thing in things { thing.move_forward(); }
}

fn main() {
    let bike = Bicycle; let car = Car; let boat = Boat;
    let travelers: [&dyn Movable; 3] = [&bike, &car, &boat];
    start_journey(&travelers);
}
```

Now you understand how Rust implements object‑oriented ideas in a safe and flexible way, without traditional inheritance. In the next chapter we will meet **advanced pattern matching** and learn how to extract data from nested structures like a professional. 🕵️‍♂️✨

![[Illustration: Ferris wearing a graduation cap and holding a glowing "Chapter 17 Master" badge. Floating around him are Lego blocks (composition), trait certificates, a Box<dyn Trait>, and a small RPG sword. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/17.4.png)