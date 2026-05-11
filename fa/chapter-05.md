# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۵: کارت شناسایی هیولاها (Structs)

### 📑 فهرست فصل
[۵.۱. هیولای من چه شکلیه؟](#۵۱-هیولای-من-چه-شکلیه)  
[۵.۱.۱. داستان: دفترچه‌ی هیولاهای فریس](#۵۱۱-داستان-دفترچهی-هیولاهای-فریس)  
[۵.۱.۲. مشکل: چند تا متغیر جداگانه](#۵۱۲-مشکل-چند-تا-متغیر-جداگانه)  
[۵.۱.۳. معرفی struct به عنوان قالب کارت شناسایی](#۵۱۳-معرفی-struct-به-عنوان-قالب-کارت-شناسایی)  
[۵.۲. فرم استخدام هیولا (تعریف Struct)](#۵۲-فرم-استخدام-هیولا-تعریف-struct)  
[۵.۲.۱. نوشتن یک struct ساده](#۵۲۱-نوشتن-یک-struct-ساده)  
[۵.۲.۲. قرارداد نام‌گذاری PascalCase](#۵۲۲-قرارداد-نام‌گذاری-pascalcase)  
[۵.۲.۳. فیلدها و نوع آن‌ها](#۵۲۳-فیلدها-و-نوع-آنها)  
[۵.۲.۴. تمرین: struct سفینه فضایی](#۵۲۴-تمرین-struct-سفینه-فضایی)  
[۵.۳. معرفی هیولای جدید (Instance)](#۵۳-معرفی-هیولای-جدید-instance)  
[۵.۳.۱. ساختن یک نمونه از struct](#۵۳۱-ساختن-یک-نمونه-از-struct)  
[۵.۳.۲. دسترسی به فیلدها با نقطه](#۵۳۲-دسترسی-به-فیلدها-با-نقطه)  
[۵.۳.۳. تغییر فیلدها (با mut)](#۵۳۳-تغییر-فیلدها-با-mut)  
[۵.۳.۴. اختصار Field Init Shorthand](#۵۳۴-اختصار-field-init-shorthand)  
[۵.۳.۵. ساختن نمونه از روی نمونه دیگر (struct update syntax)](#۵۳۵-ساختن-نمونه-از-روی-نمونه-دیگر-struct-update-syntax)  
[۵.۴. کارهایی که هیولا می‌تونه بکنه (Methods)](#۵۴-کارهایی-که-هیولا-می‌تونه-بکنه-methods)  
[۵.۴.۱. تفاوت تابع و متد](#۵۴۱-تفاوت-تابع-و-متد)  
[۵.۴.۲. نوشتن اولین متد با impl](#۵۴۲-نوشتن-اولین-متد-با-impl)  
[۵.۴.۳. پارامتر &self](#۵۴۳-پارامتر-self)  
[۵.۴.۴. متد با پارامترهای اضافی](#۵۴۴-متد-با-پارامترهای-اضافی)  
[۵.۴.۵. متد با مقدار بازگشتی](#۵۴۵-متد-با-مقدار-بازگشتی)  
[۵.۴.۶. متد تغییردهنده (&mut self)](#۵۴۶-متد-تغییردهنده-mut-self)  
[۵.۴.۷. توابع مرتبط (Associated Functions)](#۵۴۷-توابع-مرتبط-associated-functions)  
[۵.۵. پروژه: دفترچه هیولاها](#۵۵-پروژه-دفترچه-هیولاها)  
[۵.۵.۱. ساخت Vec از هیولاها](#۵۵۱-ساخت-vec-از-هیولاها)  
[۵.۵.۲. حلقه برای غرش کردن همه](#۵۵۲-حلقه-برای-غرش-کردن-همه)  
[۵.۵.۳. پیدا کردن قوی‌ترین هیولا](#۵۵۳-پیدا-کردن-قوی‌ترین-هیولا)  
[۵.۵.۴. تمرین: متد is_stronger_than](#۵۵۴-تمرین-متد-is_stronger_than)  
[۵.۶. جمع‌بندی و چالش](#۵۶-جمع‌بندی-و-چالش)  
[۵.۶.۱. مرور مفاهیم](#۵۶۱-مرور-مفاهیم)  
[۵.۶.۲. چالش: struct Student و نمره](#۵۶۲-چالش-struct-student-و-نمره)  

---

### ۵.۱. هیولای من چه شکلیه؟

#### ۵.۱.۱. داستان: دفترچه‌ی هیولاهای فریس
فریس در سفرهای فضایی‌اش با کلی موجود عجیب و غریب آشنا شده. بعضی‌هاشان غول‌پیکرند، بعضی‌هاشان کوچولو و بانمک. فریس تصمیم گرفته یک دفترچه درست کند و مشخصات هر هیولا را در آن یادداشت کند: اسمش چیست؟ چه رنگی است؟ چند تا پا دارد؟ قدرتش چقدر است؟  
این مشخصات برای هر هیولا دقیقاً مثل یک **کارت شناسایی** می‌ماند. در برنامه‌نویسی وقتی می‌خواهیم اطلاعات مربوط به یک چیز را یکجا و مرتب نگه داریم، از یک ابزار فوق‌العاده به اسم `struct` (مخفف Structure) استفاده می‌کنیم.

#### ۵.۱.۲. مشکل: چند تا متغیر جداگانه
اگر بخواهیم بدون `struct` اطلاعات یک هیولا را ذخیره کنیم، مجبوریم کلی متغیر جداگانه بسازیم:
```rust
let name = String::from("دودو");
let color = String::from("سبز");
let legs = 4;
let power = 100;
```
برای یک هیولا بد نیست. ولی اگر ده تا هیولا داشته باشیم، کلی متغیر با اسم‌های قاطی‌پاتی مثل `name2`, `color3` درست می‌شود که خیلی زود گیج‌کننده می‌شود! تازه، نمی‌توانیم همه‌ی این اطلاعات را مثل یک بسته‌ی آماده به یک تابع بدهیم.

#### ۵.۱.۳. معرفی struct به عنوان قالب کارت شناسایی
`struct` به ما اجازه می‌دهد چند تکه اطلاعات را کنار هم بگذاریم و بهشان یک اسم واحد بدهیم. در واقع `struct` مثل یک **قالب خالی کارت شناسایی** می‌ماند. اول قالب را طراحی می‌کنیم (می‌گوییم هر کارت چه بخش‌هایی دارد)، بعد با استفاده از آن قالب، کارت‌های واقعی برای هیولاهای مختلف پر می‌کنیم.  
**این یعنی تو داری یاد می‌گیری چطور اطلاعات دنیای واقعی را داخل کامپیوتر مدل کنی – گامی دیگر برای تبدیل شدن به یک جادوگر کامپیوتر!** 🧙‍♂️

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> Structها یکی از مهم‌ترین ابزارهای Rust (و بسیاری زبان‌های دیگر) هستند. آن‌ها به کودک کمک می‌کنند تا داده‌های مرتبط را گروه‌بندی کند – مهارتی فراتر از برنامه‌نویسی. کتاب رسمی Rust فصل کاملی درباره‌ی structها دارد:  
> [doc.rust-lang.org/book/ch05-00-structs.html](https://doc.rust-lang.org/book/ch05-00-structs.html)

![[Illustration: Cartoon illustration of a magical notebook open on a wooden desk. The left page shows messy scattered variables with tangled strings. The right page shows a clean, glowing ID card template with slots for "Name", "Color", "Legs", "Power". Ferris the crab stands proudly pointing at the clean page. Style: vibrant children's book, educational metaphor, soft lighting, 16:9.]](../assets/images/5.1.png)

---

### ۵.۲. فرم استخدام هیولا (تعریف Struct)

#### ۵.۲.۱. نوشتن یک struct ساده
با کلمه‌ی کلیدی `struct` شروع می‌کنیم، اسم قالب را می‌نویسیم و داخل آکولاد `{}` فیلدهایش را تعریف می‌کنیم:
```rust
struct Monster {
    name: String,
    color: String,
    legs: u8,
    power: u32,
}
```
این کد یعنی: «یک قالب جدید به اسم `Monster` داریم. هر چیزی که از این قالب ساخته شود، چهار بخش دارد: یک اسم (`String`)، یک رنگ (`String`)، تعداد پا (`u8` یعنی عدد صحیح کوچک مثبت) و قدرت (`u32`).»

#### ۵.۲.۲. قرارداد نام‌گذاری PascalCase
در Rust یک رسم قشنگ داریم: اسم `struct`ها را به صورت **PascalCase** می‌نویسیم. یعنی هر کلمه با حرف بزرگ شروع شود و فاصله نداشته باشد. مثال: `Monster`، `SpaceShip`، `StudentGrade`.  
اسم فیلدها اما با **snake_case** نوشته می‌شود: همه حروف کوچک و با زیرخط (`_`) جدا می‌شوند. مثال: `name`, `legs_count`, `fuel_amount`.

#### ۵.۲.۳. فیلدها و نوع آن‌ها
هر فیلد یک اسم و یک نوع (Type) دارد. می‌توانی از هر نوعی که تا حالا یاد گرفتی استفاده کنی: `i32`, `f64`, `bool`, `char`, `String` و حتی `struct`های دیگر! مثلاً می‌توانی یک `struct` برای مختصات بسازی و بگذاریش داخل `Monster`:
```rust
struct Coordinates {
    x: f64,
    y: f64,
}

struct Monster {
    name: String,
    position: Coordinates,
    // بقیه فیلدها...
}
```

#### ۵.۲.۴. تمرین: struct سفینه فضایی
یک `struct` به اسم `SpaceShip` تعریف کن که سه فیلد داشته باشد:
- `fuel` از نوع `u32` (سوخت باقی‌مانده)
- `passenger_count` از نوع `u8` (تعداد مسافران)
- `model` از نوع `String` (مدل سفینه)

💡 **پاسخ:**
```rust
struct SpaceShip {
    fuel: u32,
    passenger_count: u8,
    model: String,
}
```

![[Illustration: Educational infographic showing a Rust struct definition as a blueprint sheet. Fields are highlighted with colorful tags matching their data types (String=blue, u8=green, u32=orange). Ferris holds a ruler and pencil, drawing the blueprint. Style: clean, modern educational cartoon, bright colors, 16:9.]](../assets/images/5.2.png)

---

### ۵.۳. معرفی هیولای جدید (Instance)

#### ۵.۳.۱. ساختن یک نمونه از struct
حالا که قالب `Monster` را داریم، نوبت است یک هیولای واقعی ازش بسازیم. به این کار می‌گویند ساختن **نمونه (Instance)**. اسم `struct` را می‌نویسیم و داخل `{}` به هر فیلد یک مقدار می‌دهیم:
```rust
let monster1 = Monster {
    name: String::from("دودو"),
    color: String::from("سبز"),
    legs: 4,
    power: 100,
};
```
حالا `monster1` یک هیولای واقعی است که اطلاعات دودو را در خودش نگه داشته.

#### ۵.۳.۲. دسترسی به فیلدها با نقطه
برای خواندن مقدار یک فیلد، از نقطه (`.`) استفاده می‌کنیم. دقیقاً مثل وقتی که به یک آدرس ایمیل یا وب‌سایت می‌رسی:
```rust
println!("اسم هیولا: {}", monster1.name);
println!("قدرت: {}", monster1.power);
```

#### ۵.۳.۳. تغییر فیلدها (با mut)
اگر بخواهیم بعداً یک فیلد را عوض کنیم (مثلاً هیولا تمرین کند و قدرتش بیشتر شود)، باید خود نمونه را موقع ساخت با `mut` تعریف کرده باشیم:
```rust
let mut monster2 = Monster {
    name: String::from("بمبی"),
    color: String::from("قرمز"),
    legs: 2,
    power: 50,
};

monster2.power = 75;  // الان قدرت بمبی شد ۷۵
```

#### ۵.۳.۴. اختصار Field Init Shorthand
اگر قبلاً متغیرهایی ساخته باشی که اسمشان دقیقاً با اسم فیلدهای `struct` یکی باشد، می‌توانی به جای تکرار `name: name` فقط اسم متغیر را بنویسی:
```rust
let name = String::from("دودو");
let color = String::from("سبز");
let legs = 4;
let power = 100;

let monster = Monster {
    name,   // یعنی name: name
    color,  // یعنی color: color
    legs,   // یعنی legs: legs
    power,  // یعنی power: power
};
```
این کار کد را کوتاه‌تر و خواناتر می‌کند. 🧹✨

#### ۵.۳.۵. ساختن نمونه از روی نمونه دیگر (struct update syntax)
گاهی می‌خواهیم یک هیولای جدید بسازیم که خیلی شبیه یک هیولای قبلی است، فقط مثلاً اسمش فرق می‌کند. به جای نوشتن دوباره‌ی همه‌ی فیلدها، از علامت `..` استفاده می‌کنیم:
```rust
let monster2 = Monster {
    name: String::from("بمبی"),
    ..monster1   // بقیه فیلدها را از monster1 کپی کن
};
```
⚠️ **نکته‌ی مهم:** این کار باعث **انتقال مالکیت (Move)** می‌شود! یعنی اگر فیلدی مثل `name` از نوع `String` باشد (که `Copy` نیست)، بعد از این خط دیگر نمی‌توانی از `monster1.name` استفاده کنی چون مالکیتش رفته پیش `monster2`. اما فیلدهای عددی مثل `legs` و `power` چون `Copy` هستند، کپی می‌شوند و `monster1` هنوز می‌تواند ازشان استفاده کند.  
فعلاً همین را بدانید که `..` راحت است اما مراقب مالکیت باشید. (در آینده با `clone()` هم آشنا خواهید شد.)

![[Illustration: Split illustration: Left side shows a crab holding a "monster blueprint" copying data to a new card using a ".." stamp. Right side shows a warning sign: "String fields move ownership!". Ferris explains with a friendly gesture. Style: playful technical metaphor, children's book illustration, clear visual cues, 16:9.]](../assets/images/5.3.png)

---

### ۵.۴. کارهایی که هیولا می‌تونه بکنه (Methods)

#### ۵.۴.۱. تفاوت تابع و متد
تابع (Function) یک بلوک کد مستقلی است که می‌تواند پارامتر بگیرد و مقدار برگرداند (مثل `add` در فصل قبل).  
متد (Method) تابعی است که **به یک `struct` چسبیده** است. متدها با نقطه (`.`) روی نمونه‌ها صدا زده می‌شوند و اولین پارامترشان همیشه به خود نمونه اشاره دارد (معمولاً `&self`). مثل وقتی که می‌گویید «هیولا غرش کن!» به جای «غرش کن هیولا را!».

#### ۵.۴.۲. نوشتن اولین متد با impl
برای تعریف متد برای یک `struct`، از بلوک `impl` (مخفف implementation) استفاده می‌کنیم:
```rust
impl Monster {
    fn roar(&self) {
        println!("{} غرغروووو!", self.name);
    }
}
```
حالا می‌توانیم برای هر هیولایی که داریم، این متد را صدا بزنیم:
```rust
let dodo = Monster { /* ... */ };
dodo.roar();  // چاپ می‌کند: "دودو غرغروووو!"
```

#### ۵.۴.۳. پارامتر `&self`
`&self` یک مرجع غیرقابل تغییر (immutable) به نمونه‌ی جاری است. یعنی متد می‌تواند فیلدها را بخواند ولی نمی‌تواند تغییرشان بدهد. سه حالت اصلی برای `self` داریم:
🔹 `&self` : فقط خواندن (رایج‌ترین حالت)  
🔹 `&mut self` : خواندن و تغییر دادن (نیاز دارد نمونه `mut` باشد)  
🔹 `self` : گرفتن مالکیت نمونه (بعد از صدا زدن، نمونه از بین می‌رود – کمتر استفاده می‌شود)

#### ۵.۴.۴. متد با پارامترهای اضافی
می‌توانیم به متد، علاوه بر `&self`، پارامترهای دیگر هم بدهیم:
```rust
impl Monster {
    fn attack(&self, target: &str) {
        println!("{} به {} حمله کرد با قدرت {}!", self.name, target, self.power);
    }
}
```
صدا زدن:
```rust
dodo.attack("بیل");
// خروجی: دودو به بیل حمله کرد با قدرت 100!
```

#### ۵.۴.۵. متد با مقدار بازگشتی
متدها هم مثل توابع می‌توانند مقدار برگردانند:
```rust
impl Monster {
    fn power_level(&self) -> u32 {
        self.power
    }
}
```

#### ۵.۴.۶. متد تغییردهنده (`&mut self`)
اگر بخواهیم متد بتواند فیلدهای نمونه را تغییر دهد (مثلاً قدرت هیولا را زیاد کند)، باید از `&mut self` استفاده کنیم و خود نمونه هم `mut` باشد:
```rust
impl Monster {
    fn heal(&mut self, amount: u32) {
        self.power += amount;
        println!("{} قدرت گرفت و شد {}!", self.name, self.power);
    }
}
```
استفاده:
```rust
let mut bombi = Monster { /* ... */ };
bombi.heal(20);
```

#### ۵.۴.۷. توابع مرتبط (Associated Functions)
گاهی به تابعی نیاز داریم که روی نمونه‌ی خاصی کار نکند، بلکه یک کار کلی برای `struct` انجام بدهد. معروف‌ترین مثال، تابع `new` است که یک نمونه‌ی جدید می‌سازد. این توابع را **توابع مرتبط** می‌نامیم و با `::` (دابل کولون) صدا می‌زنیم:
```rust
impl Monster {
    fn new(name: String, color: String, legs: u8, power: u32) -> Monster {
        Monster {
            name,
            color,
            legs,
            power,
        }
    }
}
```
استفاده:
```rust
let dodo = Monster::new(
    String::from("دودو"),
    String::from("سبز"),
    4,
    100,
);
```
این روش خیلی تمیزتر از نوشتن مستقیم فیلدها در `main` است و حس یک «کارخانه‌ی ساخت هیولا» را می‌دهد! 🏭

![[Illustration: Cartoon scene showing a "Method Factory" conveyor belt. Crabs input raw monster parts, a machine labeled "impl Monster" adds behaviors (roar, attack, heal) via &self/&mut self tags, and finished monsters roll out with speech bubbles. Ferris operates a control panel. Style: dynamic, educational, bright colors, 16:9.]](../assets/images/5.4.png)

---

### ۵.۵. پروژه: دفترچه هیولاها
حالا با هم یک برنامه‌ی کوچک می‌نویسیم که لیستی از هیولاها را نگه می‌دارد و کارهایی رویشان انجام می‌دهد.

#### ۵.۵.۱. ساخت Vec از هیولاها
اول یک `Vec` (وکتور) از `Monster` می‌سازیم. وکتور مثل یک **کوله‌پشتی جادویی** است که می‌توانی هی در آن هیولا اضافه کنی و اندازه‌اش خود به خود بزرگ می‌شود:
```rust
let mut monster_list = Vec::new();

monster_list.push(Monster::new(
    String::from("دودو"),
    String::from("سبز"),
    4,
    100,
));

monster_list.push(Monster::new(
    String::from("بمبی"),
    String::from("قرمز"),
    2,
    75,
));

monster_list.push(Monster::new(
    String::from("زرزر"),
    String::from("زرد"),
    6,
    120,
));
```
*(نکته: `Vec` در فصل ۸ کامل آموزش داده می‌شود، ولی فعلاً فقط بدانید که مثل یک لیست قابل رشد است که با `push` به آن عضو اضافه می‌کنیم.)*

#### ۵.۵.۲. حلقه برای غرش کردن همه
حالا می‌خواهیم روی همه‌ی هیولاهای داخل لیست بچرخیم و از هرکسی بخواهیم غرش کند. برای این کار از یک حلقه‌ی جدید به نام `for` استفاده می‌کنیم که به طور خودکار به ما یک یک اعضای لیست را می‌دهد:
```rust
for monster in &monster_list {
    monster.roar();
}
```
(علامت `&` جلوی `monster_list` یعنی ما فقط قرض می‌گیریم و لیست را مالک نمی‌شویم – درست مثل کارت امانت فصل ۴.)

#### ۵.۵.۳. پیدا کردن قوی‌ترین هیولا
یک تابع می‌نویسیم که قوی‌ترین هیولا را پیدا کند (یعنی بیشترین `power` را داشته باشد):
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
و در `main`:
```rust
let champ = strongest(&monster_list);
println!("قوی‌ترین هیولا: {} با قدرت {}", champ.name, champ.power);
```

#### ۵.۵.۴. تمرین: متد `is_stronger_than`
به `struct Monster` یک متد به اسم `is_stronger_than` اضافه کن که یک `&Monster` دیگر بگیرد و `true` برگرداند اگر قدرت خودش از آن یکی بیشتر باشد.

💡 **پاسخ:**
```rust
impl Monster {
    fn is_stronger_than(&self, other: &Monster) -> bool {
        self.power > other.power
    }
}
```
استفاده:
```rust
if dodo.is_stronger_than(&bombi) {
    println!("دودو قوی‌تر از بمبی است!");
}
```

![[Illustration: A cozy notebook open to a "Monster Roster" page. Each entry shows a mini ID card with a cartoon monster sketch and stats. A golden trophy icon highlights the strongest monster. Ferris sits on the desk stamping "Approved" with a smile. Style: warm, inviting children's book illustration, detailed UI metaphor, 16:9.]](../assets/images/5.5.png)

---

### ۵.۶. جمع‌بندی و چالش

#### ۵.۶.۱. مرور مفاهیم
در این فصل یاد گرفتی:  
✅ `struct` قالبی برای دسته‌بندی داده‌های مرتبط است.  
✅ نمونه‌ها با `let x = StructName { fields };` ساخته می‌شوند.  
✅ دسترسی به فیلدها با نقطه (`.`) انجام می‌شود.  
✅ متدها در بلوک `impl` تعریف می‌شوند و اولین پارامترشان `self` (یا `&self` یا `&mut self`) است.  
✅ توابع مرتبط (مثل `new`) با `::` صدا زده می‌شوند.  
✅ می‌توانیم از `..` برای کپی کردن فیلدها از نمونه‌ی دیگر استفاده کنیم (با دقت در مورد مالکیت!).  
✅ حلقه‌ی `for` راهی آسان برای پیمایش لیست‌هاست.

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> استفاده از struct و متدها ممکن است در ابتدا کمی عجیب به نظر برسد، اما با تمرین کاملاً طبیعی می‌شود. هر بار که یک struct برای مدل کردن چیزی در دنیای واقعی می‌سازی، در حقیقت مثل یک مهندس نرم‌افزار فکر می‌کنی. اگر هنوز در بعضی بخش‌ها احساس ابهام داری، نگران نباش – در فصل‌های بعدی بارها از structها استفاده خواهی کرد.

#### ۵.۶.۲. چالش: struct Student و نمره
یک `struct` به اسم `Student` با فیلدهای `name: String` و `grade: f64` بساز. سپس یک متد به نام `passed(&self) -> bool` بنویس که اگر `grade >= 10.0` بود `true` برگرداند، در غیر این صورت `false`.  
بعد یک وکتور از چند دانش‌آموز بساز و همه‌ی کسانی که قبول شده‌اند را چاپ کن.

💡 **پاسخ نمونه:**
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
        Student::new(String::from("سارا"), 18.5),
        Student::new(String::from("رضا"), 9.0),
        Student::new(String::from("مریم"), 14.0),
    ];

    for student in &students {
        if student.passed() {
            println!("{} قبول شد با نمره {}", student.name, student.grade);
        } else {
            println!("{} نیاز به تلاش بیشتر دارد.", student.name);
        }
    }
}
```
حالا تو می‌دانی چطور داده‌های مرتبط را در قالب `struct` سازماندهی کنی و برایشان رفتار (متد) تعریف کنی. در فصل بعد با `enum` و `match` آشنا می‌شویم و یاد می‌گیریم چطور با حالت‌های مختلف یک مقدار (مثل وضعیت بازی، آب و هوا، یا رنگ چراغ) کار کنیم. 🌈✨

![[Illustration: Ferris wearing a graduation cap, holding a glowing "Chapter 5 Complete" badge. Floating around him are mini structs, impl blocks, and &self tags turning into a neat organized library. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/5.6.png)
