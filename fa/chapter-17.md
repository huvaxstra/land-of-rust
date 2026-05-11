# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۱۷: آیا Rust یک ربات ترنسفورمر است؟ (شی‌گرایی به سبک Rust)

### 📑 فهرست فصل
[۱۷.۱. ربات‌های سنتی (Inheritance)](#۱۷۱-ربات‌های-سنتی-inheritance)  
[۱۷.۱.۱. داستان: ربات پدر و ربات پسر](#۱۷۱۱-داستان-ربات-پدر-و-ربات-پسر)  
[۱۷.۱.۲. ارث‌بری در زبان‌های دیگر (مثل جاوا)](#۱۷۱۲-ارث‌بری-در-زبان‌های-دیگر-مثل-جاوا)  
[۱۷.۱.۳. مشکلات ارث‌بری](#۱۷۱۳-مشکلات-ارث‌بری)  
[۱۷.۲. روش Rust (Composition & Traits)](#۱۷۲-روش-rust-composition--traits)  
[۱۷.۲.۱. ترکیب (Composition) به جای ارث‌بری](#۱۷۲۱-ترکیب-composition-به-جای-ارث‌بری)  
[۱۷.۲.۲. اشتراک رفتار با Traits](#۱۷۲۲-اشتراک-رفتار-با-traits)  
[۱۷.۲.۳. تفاوت Rust با ارث‌بری سنتی](#۱۷۲۳-تفاوت-rust-با-ارث‌بری-سنتی)  
[۱۷.۲.۴. تمرین: trait Sound و پیاده‌سازی برای چند نوع](#۱۷۲۴-تمرین-trait-sound-و-پیاده‌سازی-برای-چند-نوع)  
[۱۷.۳. پروژه: شبیه‌سازی یک بازی ساده](#۱۷۳-پروژه-شبیه‌سازی-یک-بازی-ساده)  
[۱۷.۳.۱. تعریف trait Attack](#۱۷۳۱-تعریف-trait-attack)  
[۱۷.۳.۲. تعریف struct Health](#۱۷۳۲-تعریف-struct-health)  
[۱۷.۳.۳. تعریف struct‌های Warrior, Mage, Archer](#۱۷۳۳-تعریف-struct‌های-warrior-mage-archer)  
[۱۷.۳.۴. پیاده‌سازی Attack برای هر کدام](#۱۷۳۴-پیاده‌سازی-attack-برای-هر-کدام)  
[۱۷.۳.۵. استفاده از trait object (Box<dyn Attack>)](#۱۷۳۵-استفاده-از-trait-object-boxdyn-attack)  
[۱۷.۴. جمع‌بندی و چالش](#۱۷۴-جمع‌بندی-و-چالش)  
[۱۷.۴.۱. مرور مفاهیم](#۱۷۴۱-مرور-مفاهیم)  
[۱۷.۴.۲. چالش: trait Movable](#۱۷۴۲-چالش-trait-movable)

---

### ۱۷.۱. ربات‌های سنتی (Inheritance)

#### ۱۷.۱.۱. داستان: ربات پدر و ربات پسر
در خیلی از کارخانه‌های اسباب‌بازی، وقتی می‌خواهند یک ربات جدید بسازند، اول یک «ربات پدر» می‌سازند که کارهای پایه مثل راه رفتن و حرف زدن را بلد باشد. بعد می‌گویند: «ربات پسر همان کارها را بلد است، فقط بال هم دارد!» این روش که بچه همه‌ی ویژگی‌های پدر را به ارث می‌برد، در برنامه‌نویسی **ارث‌بری (Inheritance)** نامیده می‌شود. 🤖👨‍👦

#### ۱۷.۱.۲. ارث‌بری در زبان‌های دیگر (مثل جاوا)
در زبان‌هایی مثل جاوا یا ++C، این کار خیلی رایج است:
```java
// مثال فرضی از زبان جاوا
class Robot {
    void walk() { /* راه رفتن */ }
}

class FlyingRobot extends Robot {
    void fly() { /* پرواز کردن */ }
}
```
حالا `FlyingRobot` هم `walk` را دارد (چون از پدرش گرفته) و هم `fly` را. در نگاه اول خیلی قشنگ است، اما...

#### ۱۷.۱.۳. مشکلات ارث‌بری
ارث‌بری چند تا مشکل بزرگ دارد که Rust عمداً از آن فرار کرده است:
🔸 **سلسله‌مراتب خشک:** اگر بعداً بخواهیم رباتی بسازیم که هم پرواز کند هم شنا کند، باید از دو پدر ارث‌بری کند که باعث سردرگمی می‌شود (مشکل الماس!).  
🔸 **ارث‌بری ناخواسته:** اگر یک «پنگوئن» از کلاس «پرنده» ارث‌بری کند، متد `fly` را هم به ارث می‌برد در حالی که پنگوئن اصلاً نمی‌تواند پرواز کند!  
🔸 **شکنندگی:** اگر مهندس ربات پدر یک تغییر کوچک بدهد، ممکن است ناگهان کد ربات پسر خراب شود.

Rust می‌گوید: «به جای سلسله‌مراتب سفت‌وسخت، بیایید با قطعات لگو (Composition) و گواهی‌نامه‌های مهارت (Traits) کار کنیم!» 🧩✨  
**این رویکرد یعنی تو به جای تقلید کورکورانه، می‌توانی رفتارها را مثل قطعات یک جعبه ابزار ترکیب کنی – یک جادوگر کامپیوتر چنین می‌کند.** 🧙‍♂️

![[Illustration: A split cartoon comparison. Left side: a rigid, tangled family tree of robots labeled "Inheritance (Messy)". Right side: neat Lego blocks labeled "Composition" being snapped together. Ferris the crab points happily at the Lego side. Style: educational vector illustration, bright colors, clear visual metaphor, 16:9.]](../assets/images/17.1.png)

---

### ۱۷.۲. روش Rust (Composition & Traits)

#### ۱۷.۲.۱. ترکیب (Composition) به جای ارث‌بری
در Rust به جای اینکه بگوییم «ربات جنگجو **نوعی** ربات است»، می‌گوییم «ربات جنگجو **دارای** یک موتور، یک شمشیر و یک سپر است». به این می‌گوییم **ترکیب (Composition)**:
```rust
struct Engine;      // موتور
struct Sword;       // شمشیر
struct Shield;      // سپر

struct CombatRobot {
    engine: Engine,
    weapon: Sword,
    shield: Shield,
}
```
اگر بعداً بخواهیم ربات پرنده بسازیم، فقط کافی است یک قطعه‌ی `Wing` به آن اضافه کنیم. نیازی به تغییر کل سلسله‌مراتب نیست. ترکیب مثل ساختن اسباب‌بازی با لگو است: آزادی عمل کامل! 🧱

#### ۱۷.۲.۲. اشتراک رفتار با Traits
اما اگر چند ربات مختلف بخواهند یک کار مشترک انجام دهند چه؟ مثلاً همگی بخواهند آژیر بکشند؟ اینجا **Trait** وارد می‌شود. Trait مثل یک گواهی‌نامه‌ی مهارت است که می‌گوید: «این ربات بلد است آژیر بزند.»
```rust
trait MakeSound {
    fn make_sound(&self);
}

struct Dog;
impl MakeSound for Dog {
    fn make_sound(&self) { println!("هاپ! هاپ!"); }
}

struct Car;
impl MakeSound for Car {
    fn make_sound(&self) { println!("بوق بوق!"); }
}
```
حالا هر کدام به روش خودش صدا می‌دهد، ولی هر دو گواهی‌نامه‌ی `MakeSound` را دارند! 🏅

#### ۱۷.۲.۳. تفاوت Rust با ارث‌بری سنتی
🔹 در Rust می‌توانی برای یک نوع، هر تعداد Trait که دوست داری پیاده‌سازی کنی.  
🔹 هیچ سلسله‌مراتب اجباری وجود ندارد.  
🔹 دقیقاً مشخص است هر قطعه چه قابلیتی دارد، نه اینکه یک بسته‌ی بزرگ و گیج‌کننده را به ارث ببری.

#### ۱۷.۲.۴. تمرین: trait Sound و پیاده‌سازی برای چند نوع
یک Trait به اسم `Sound` با متد `make_sound(&self)` تعریف کن. برای `Cat`، `Cow` و `Phone` پیاده‌سازی‌اش کن. بعد در یک `Vec<Box<dyn Sound>>` بریزشان و صدایشان را در بیاور.

💡 **پاسخ نمونه:**
```rust
trait Sound { fn make_sound(&self); }

struct Cat; impl Sound for Cat { fn make_sound(&self) { println!("میو! 🐱"); } }
struct Cow; impl Sound for Cow { fn make_sound(&self) { println!("مــاـاـا! 🐮"); } }
struct Phone; impl Sound for Phone { fn make_sound(&self) { println!("زنگ زنگ! 📱"); } }

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

### ۱۷.۳. پروژه: شبیه‌سازی یک بازی ساده

حالا بیا اینها را در یک بازی نقش‌آفرینی کوچک تست کنیم! 🎮⚔️

#### ۱۷.۳.۱. تعریف `trait Attack`
اول یک گواهی‌نامه می‌سازیم که بگوید «هر چیزی که این را داشته باشد، می‌تواند حمله کند»:
```rust
trait Attack {
    fn attack(&self, target: &mut Health);
}
```

#### ۱۷.۳.۲. تعریف `struct Health`
یک ساختار ساده برای سلامتی (`Health`) که فقط یک عدد `hp` دارد و می‌تواند آسیب ببیند:
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

#### ۱۷.۳.۳. تعریف `struct`های `Warrior`, `Mage`, `Archer`
سه قهرمان متفاوت می‌سازیم:
```rust
struct Warrior { power: i32 }
struct Mage { mana: i32 }
struct Archer { arrows: i32 }
```

#### ۱۷.۳.۴. پیاده‌سازی `Attack` برای هر کدام
هر کدام به سبک خودش حمله می‌کند:
```rust
impl Attack for Warrior {
    fn attack(&self, target: &mut Health) {
        println!("⚔️ جنگجو با قدرت {} ضربه زد!", self.power);
        target.take_damage(self.power);
    }
}

impl Attack for Mage {
    fn attack(&self, target: &mut Health) {
        let damage = self.mana / 2;
        println!("🔮 جادوگر با {} آسیب طلسم کرد!", damage);
        target.take_damage(damage);
    }
}

impl Attack for Archer {
    fn attack(&self, target: &mut Health) {
        let damage = self.arrows;
        println!("🏹 کماندار {} تیر پرتاب کرد!", damage);
        target.take_damage(damage);
    }
}
```

#### ۱۷.۳.۵. استفاده از trait object (`Box<dyn Attack>`)
حالا می‌خواهیم یک لشکر از قهرمان‌های مختلف داشته باشیم و به یک دشمن حمله کنیم. چون اندازه‌ی `Warrior`، `Mage` و `Archer` با هم فرق دارد، نمی‌توانیم مستقیم در یک آرایه بگذاریمشان. راه حل؟ استفاده از **Trait Object** و `Box`:
```rust
fn main() {
    let mut enemy = Health::new(80); // دشمن با ۸۰ جان

    let heroes: Vec<Box<dyn Attack>> = vec![
        Box::new(Warrior { power: 25 }),
        Box::new(Mage { mana: 40 }),
        Box::new(Archer { arrows: 15 }),
    ];

    for hero in heroes {
        hero.attack(&mut enemy);
        println!("وضعیت دشمن: {:?}", enemy);
        if !enemy.is_alive() {
            println!("💀 دشمن شکست خورد!");
            break;
        }
    }
}
```
📌 **نکته‌ی مهم:** `dyn Attack` یعنی «در این جعبه، هر چیزی که Trait را داشته باشد می‌توانی بگذاری». `Box` آن را می‌برد در حافظه‌ی پویا (`heap`) تا اندازه‌اش مهم نباشد. این‌طوری می‌توانیم انواع مختلف را در یک لیست نگه داریم و یکجا روی آنها حلقه بزنیم! 🎉

![[Illustration: Cartoon RPG battle scene. Three heroes (Warrior, Mage, Archer) stand on one side, each holding a glowing "Box<dyn Attack>" badge. On the other side, a cartoon monster has a health bar showing 80 → 55 → 35. Ferris acts as a referee holding a flag. Style: vibrant, dynamic children's book illustration, 16:9.]](../assets/images/17.3.png)

---

### ۱۷.۴. جمع‌بندی و چالش

#### ۱۷.۴.۱. مرور مفاهیم
✅ Rust ارث‌بری کلاس‌محور ندارد.  
✅ به جای آن از **ترکیب** (Composition) برای داده‌ها و **Traits** برای رفتارها استفاده می‌کند.  
✅ `Box<dyn Trait>` به ما اجازه می‌دهد انواع مختلفی که یک Trait مشترک دارند را کنار هم در یک کالکشن ذخیره کنیم.  
✅ این روش برنامه‌ها را منعطف‌تر، ایمن‌تر و تمیزتر از ارث‌بری سنتی می‌کند.

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> درک تفاوت بین ترکیب و ارث‌بری ممکن است در ابتدا کمی انتزاعی به نظر برسد. حتی توسعه‌دهندگان باتجربه هم گاهی بحث می‌کنند که کدام روش مناسب‌تر است. مهم این است که بدانی Rust به تو آزادی می‌دهد بدون اینکه تو را مجبور به ساخت سلسله‌مراتب خشک کند. با تمرین روی پروژه‌های کوچک، این مفهوم برایت شفاف می‌شود.

#### ۱۷.۴.۲. چالش: trait Movable
یک Trait به اسم `Movable` با متد `move_forward(&self)` تعریف کن. برای سه ساختار `Bicycle`، `Car` و `Boat` این Trait را پیاده‌سازی کن (مثلاً دوچرخه چرخ‌ها را می‌چرخاند، ماشین موتور روشن می‌کند، قایق پارو می‌زند). سپس یک تابع `start_journey` بنویس که یک آرایه از `&dyn Movable` دریافت کند و از هر کدام بخواهد حرکت کند.

💡 **پاسخ نمونه:**
```rust
trait Movable { fn move_forward(&self); }

struct Bicycle; impl Movable for Bicycle { fn move_forward(&self) { println!("🚲 چرخ‌ها می‌چرخند..."); } }
struct Car; impl Movable for Car { fn move_forward(&self) { println!("🚗 موتور روشن شد، بریم!"); } }
struct Boat; impl Movable for Boat { fn move_forward(&self) { println!("⛵ پاروها در آب می‌خورند..."); } }

fn start_journey(things: &[&dyn Movable]) {
    for thing in things { thing.move_forward(); }
}

fn main() {
    let bike = Bicycle; let car = Car; let boat = Boat;
    let travelers: [&dyn Movable; 3] = [&bike, &car, &boat];
    start_journey(&travelers);
}
```

حالا تو فهمیدی که Rust چطور بدون ارث‌بری سنتی، مفاهیم شی‌گرایی را به شکلی امن و انعطاف‌پذیر پیاده‌سازی می‌کند. در فصل بعد، با **الگوهای پیشرفته (Advanced Pattern Matching)** آشنا می‌شویم و یاد می‌گیریم چطور مثل یک حرفه‌ای، داده‌ها را از دل ساختارهای تو در تو بیرون بکشیم. 🕵️‍♂️✨

![[Illustration: Ferris wearing a graduation cap and holding a glowing "Chapter 17 Master" badge. Floating around him are Lego blocks (composition), trait certificates, a Box<dyn Trait>, and a small RPG sword. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/17.4.png)
