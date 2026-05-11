# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۱۸: نقشه‌های پیچیده‌ی گنج (Pattern Matching پیشرفته)

### 📑 فهرست فصل
[۱۸.۱. پازل‌های سخت: بیرون کشیدن از دل ساختارها](#۱۸۱-پازل‌های-سخت-بیرون-کشیدن-از-دل-ساختارها)  
[۱۸.۱.۱. داستان: جعبه‌های تو در تو](#۱۸۱۱-داستان-جعبه‌های-تو-در-تو)  
[۱۸.۱.۲. تخریب (Destructuring) Struct](#۱۸۱۲-تخریب-destructuring-struct)  
[۱۸.۱.۳. تخریب Enum](#۱۸۱۳-تخریب-enum)  
[۱۸.۱.۴. تخریب Tuple](#۱۸۱۴-تخریب-tuple)  
[۱۸.۱.۵. تخریب در حلقه for](#۱۸۱۵-تخریب-در-حلقه-for)  
[۱۸.۱.۶. تمرین: تخریب یک Struct تو در تو](#۱۸۱۶-تمرین-تخریب-یک-struct-تو-در-تو)  
[۱۸.۲. الگوهای نفی و شرط](#۱۸۲-الگوهای-نفی-و-شرط)  
[۱۸.۲.۱. نادیده گرفتن با _ و ..](#۱۸۲۱-نادیده-گرفتن-با-_-و-)  
[۱۸.۲.۲. شرط در الگو (Match Guard)](#۱۸۲۲-شرط-در-الگو-match-guard)  
[۱۸.۲.۳. عملگر @ برای Bind کردن](#۱۸۲۳-عملگر--برای-bind-کردن)  
[۱۸.۲.۴. الگوهای | (یا)](#۱۸۲۴-الگوهای--یا)  
[۱۸.۲.۵. تمرین: Match Guard برای اعداد](#۱۸۲۵-تمرین-match-guard-برای-اعداد)  
[۱۸.۳. پروژه: پردازش دستورات یک بازی](#۱۸۳-پروژه-پردازش-دستورات-یک-بازی)  
[۱۸.۳.۱. تعریف enum Command](#۱۸۳۱-تعریف-enum-command)  
[۱۸.۳.۲. تابع parse_command](#۱۸۳۲-تابع-parse_command)  
[۱۸.۳.۳. اجرای دستور با match و guard](#۱۸۳۳-اجرای-دستور-با-match-و-guard)  
[۱۸.۴. جمع‌بندی و چالش](#۱۸۴-جمع‌بندی-و-چالش)  
[۱۸.۴.۱. مرور مفاهیم](#۱۸۴۱-مرور-مفاهیم)  
[۱۸.۴.۲. چالش: استخراج از Option<Vec<i32>>](#۱۸۴۲-چالش-استخراج-از-optionvec-i32)  

---

### ۱۸.۱. پازل‌های سخت: بیرون کشیدن از دل ساختارها

#### ۱۸.۱.۱. داستان: جعبه‌های تو در تو
فریس یک نقشه‌ی گنج قدیمی و خاک‌گرفته پیدا کرده است. 🗺️✨ ولی این نقشه یک رمز دارد: گنج در یک جعبه است، آن جعبه در یک صندوقچه است، صندوقچه در یک خزانه‌ی بزرگ است و کلید خزانه هم پیش یک پرنده‌ی فضایی است! فریس نمی‌تواند همه‌ی این لایه‌ها را یکی یکی باز کند؛ وقتش تلف می‌شود. خوشبختانه، فریس یک قدرت جادویی دارد: **الگویابی (Pattern Matching)**. با یک حرکت سریع، می‌تواند کل ساختار را بشکند و گنج را مستقیم از دل جعبه‌ها بیرون بکشد. در Rust به این کار **تخریب (Destructuring)** می‌گوییم. نترس، قرار نیست چیزی خراب شود! منظور فقط این است که ساختار را باز می‌کنیم تا به داده‌های داخلش برسیم.  
**این یعنی تو می‌توانی مثل یک کارآگاه حرفه‌ای، هر ساختار پیچیده‌ای را تکه‌تکه کنی و به گنج درونش برسی – جادوگر کامپیوتر چنین قدرتی دارد!** 🧙‍♂️

![[Illustration: A cartoon treasure map on a wooden desk. Glowing nested boxes (small box inside medium box inside big chest) float above the map. A pair of glowing magic scissors labeled "Destructuring" cuts through the layers, revealing a shiny gold coin inside. Ferris the crab watches with excited eyes, holding a magnifying glass. Style: whimsical children's book illustration, bright, adventurous, 16:9.]](../assets/images/18.1.png)

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> الگوهای پیشرفته یکی از قدرتمندترین ویژگی‌های Rust هستند که به کودکان کمک می‌کنند تا داده‌های درون ساختارها را به زیبایی استخراج کنند. اگر کودک در درک `@` یا `_` مشکل داشت، نگران نباشید – در پروژه‌های بعدی بارها از آن‌ها استفاده خواهد شد. کتاب رسمی Rust فصل کاملی درباره‌ی الگوها دارد:  
> [doc.rust-lang.org/book/ch18-00-patterns.html](https://doc.rust-lang.org/book/ch18-00-patterns.html)

#### ۱۸.۱.۲. تخریب (Destructuring) Struct
فرض کن یک `struct` به اسم `Point` داری که مختصات یک نقطه را نگه می‌دارد. می‌توانی با یک خط کد، فیلدهایش را باز کنی و در متغیرهای جدید بریزی:
```rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p = Point { x: 10, y: 20 };
    
    // روش کامل: اسم فیلد، دو نقطه، اسم متغیر جدید
    let Point { x: a, y: b } = p;
    println!("a = {}, b = {}", a, b);
    
    // روش خلاصه: اگر اسم متغیر جدید با اسم فیلد یکی باشد
    let Point { x, y } = p;
    println!("x = {}, y = {}", x, y);
}
```
اگر فقط به یکی از فیلدها نیاز داری و بقیه برایت مهم نیستند، می‌توانی بقیه را با `..` نادیده بگیری:
```rust
let Point { x, .. } = p; // فقط x را می‌گیرد، y را ول می‌کند
println!("فقط x = {}", x);
```

#### ۱۸.۱.۳. تخریب Enum
در فصل ۶ یاد گرفتی که `enum` می‌تواند حالت‌های مختلفی داشته باشد. `match` بهترین ابزار برای باز کردن این حالت‌هاست. بیا یک `enum` پیام‌های فضایی را ببینیم:
```rust
enum Message {
    Quit,                       // بدون داده
    Move { x: i32, y: i32 },    // یک struct ناشناس
    Write(String),              // یک رشته
    ChangeColor(u8, u8, u8),    // یک تاپل
}

fn process(msg: Message) {
    match msg {
        Message::Quit => println!("👋 خروج از برنامه"),
        Message::Move { x, y } => println!("🚀 حرکت به سمت ({}, {})", x, y),
        Message::Write(text) => println!("📝 نوشتن: {}", text),
        Message::ChangeColor(r, g, b) => {
            println!("🎨 تغییر رنگ به ({}, {}, {})", r, g, b);
        }
    }
}
```
ببین چقدر راحت داده‌های تو در تو را بیرون کشیدیم! `match` خودش می‌فهمد هر حالت چه شکلی است و دقیقاً همان چیزهایی که در آن است را به تو می‌دهد.

#### ۱۸.۱.۴. تخریب Tuple
تاپل‌ها هم خیلی راحت تخریب می‌شوند:
```rust
let t = (1, 2, 3);
let (x, y, z) = t;
println!("x={}, y={}, z={}", x, y, z);
```
حتی می‌توانی در پارامترهای یک تابع هم تاپل را همان اول باز کنی:
```rust
fn print_coordinates(&(x, y): &(i32, i32)) {
    println!("مختصات: ({}, {})", x, y);
}
```

#### ۱۸.۱.۵. تخریب در حلقه `for`
این قابلیت در حلقه‌های `for` خیلی کاربرد دارد، مخصوصاً وقتی با `HashMap` کار می‌کنی:
```rust
let points = vec![(0, 0), (1, 2), (3, 4)];
for (x, y) in points {
    println!("نقطه‌ی بعدی: ({}, {})", x, y);
}
```
هر بار که حلقه تکرار می‌شود، یک تاپل از لیست می‌آید بیرون، و `(x, y)` خودشان را می‌گذارند در مقادیرش. جادویی نیست، فقط Rust باهوش است! 😉

#### ۱۸.۱.۶. تمرین: تخریب یک Struct تو در تو
یک `struct` به اسم `Person` با فیلدهای `name: String` و `address: Address` تعریف کن. `Address` خودش یک `struct` با فیلدهای `city: String` و `zip: u32` است. یک نمونه `Person` بساز و با **یک خط تخریب**، هم `name` و هم `city` را مستقیم بیرون بکش و چاپ کن.

💡 **پاسخ نمونه:**
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
        name: String::from("فریس"),
        address: Address {
            city: String::from("شهر کراب"),
            zip: 12345,
        },
    };
    
    // تخریب تودرتو: name را مستقیم می‌گیریم و از داخل address فقط city را
    let Person { name, address: Address { city, .. } } = person;
    
    println!("{} در شهر {} زندگی می‌کند.", name, city);
}
```
💡 دقت کن: `address: Address { city, .. }` یعنی برو در فیلد `address`، آن را همان‌طور که از نوع `Address` انتظار داریم باز کن، ولی فقط `city` را بردار و بقیه را ول کن!

![[Illustration: A 3D puzzle cube being taken apart layer by layer. Each layer reveals a smaller cube inside, finally revealing a tiny star. Ferris stands on a stack of books, wearing a detective hat and holding a magnifying glass. Style: educational vector, bright colors, clear visual metaphor, 16:9.]](../assets/images/18.2.png)

---

### ۱۸.۲. الگوهای نفی و شرط

گاهی وقت‌ها هنگام الگویابی، می‌خواهیم یک سری چیزها را نادیده بگیریم یا فقط وقتی الگو جواب بدهد که یک شرط اضافه هم برقرار باشد. اینجاست که جادوی `match` کامل می‌شود! 🪄

#### ۱۸.۲.۱. نادیده گرفتن با `_` و `..`
🔹 `_` (زیرخط): مثل سطل زباله‌ی الگوهاست. هر چیزی که در آن بریزیم، نادیده گرفته می‌شود.  
🔹 `..` : بقیه‌ی فیلدهای یک `struct` یا بقیه‌ی اعضای یک تاپل/آرایه را ول می‌کند.

```rust
struct Point3D { x: i32, y: i32, z: i32 }
let p = Point3D { x: 1, y: 2, z: 3 };
let Point3D { x, .. } = p; // فقط x مهم است، y و z فرقی ندارند

let numbers = (1, 2, 3, 4, 5);
let (first, .., last) = numbers; // فقط اولین و آخرین
println!("اول: {}, آخر: {}", first, last);
```

#### ۱۸.۲.۲. شرط در الگو (Match Guard)
گاهی یک الگو به تنهایی کافی نیست. مثلاً می‌خواهی بگویی «اگر عدد زوج بود» یا «اگر طول رشته بیشتر از ۵ بود». این کار را با **Match Guard** انجام می‌دهیم: یک `if` که دقیقاً بعد از الگو می‌آید.
```rust
let num = Some(4);

match num {
    Some(x) if x % 2 == 0 => println!("{} عدد زوج است!", x),
    Some(x) => println!("{} عدد فرد است.", x),
    None => println!("هیچ عددی وجود ندارد."),
}
```
⚠️ ترتیب مهم است! اگر اول `Some(x)` را بدون `if` بنویسی، همیشه همان اجرا می‌شود و شرط هیچ‌وقت چک نمی‌شود.

#### ۱۸.۲.۳. عملگر `@` برای Bind کردن
علامت `@` (ات ساین) یک ابزار فوق‌العاده است: همزمان که یک الگو را بررسی می‌کند، کل مقداری که با آن الگو جور شده را در یک متغیر ذخیره می‌کند.
مثلاً می‌خواهیم بدانیم یک عدد در محدوده‌ی ۱ تا ۱۰ است یا نه، و همزمان خود عدد را هم داشته باشیم:
```rust
let x = 5;

match x {
    num @ 1..=10 => println!("{} در محدوده‌ی ۱ تا ۱۰ قرار دارد.", num),
    _ => println!("{} خارج از محدوده است.", x),
}
```
اینجا `num` همان مقدار `x` است، ولی فقط اگر در بازه‌ی `1..=10` باشد وارد این شاخه می‌شود.

#### ۱۸.۲.۴. الگوهای `|` (یا)
اگر چند تا الگو کار یکسانی انجام می‌دهند، لازم نیست برایشان شاخه‌های جدا بنویسی. می‌توانی با `|` (خط عمودی) ترکیبشان کنی:
```rust
let x = 2;

match x {
    1 | 2 => println!("یکی از اعداد ۱ یا ۲."),
    3 => println!("عدد ۳."),
    _ => println!("یک چیز دیگر."),
}
```

#### ۱۸.۲.۵. تمرین: Match Guard برای اعداد
برنامه‌ای بنویس که یک عدد از کاربر بگیرد. با `match` و `guard` تشخیص بدهد که:
- اگر بین ۱ تا ۱۰ بود → چاپ کند «کوچک».
- اگر بین ۱۱ تا ۲۰ بود → چاپ کند «متوسط».
- در غیر این صورت → چاپ کند «بزرگ یا خارج از محدوده».

💡 **پاسخ نمونه:**
```rust
use std::io;

fn main() {
    let mut input = String::new();
    println!("یک عدد وارد کن:");
    io::stdin().read_line(&mut input).unwrap();
    let num: i32 = input.trim().parse().unwrap();

    match num {
        n if (1..=10).contains(&n) => println!("عدد {} کوچک است. 👶", n),
        n if (11..=20).contains(&n) => println!("عدد {} متوسط است. 👦", n),
        _ => println!("عدد {} بزرگ است یا اصلاً در محدوده نیست. 🌳", num),
    }
}
```
💡 `(1..=10).contains(&n)` یک راه تمیز برای چک کردن عضویت در یک بازه است!

---

### ۱۸.۳. پروژه: پردازش دستورات یک بازی

حالا وقتش است همه‌ی این ابزارها را در یک پروژه‌ی واقعی امتحان کنیم! 🎮 بیا یک سیستم فرمان ساده برای یک بازی متنی بسازیم. کاربر دستوراتی مثل `/go north` یا `/attack dragon 50` تایپ می‌کند و برنامه آن‌ها را می‌فهمد و اجرا می‌کند.

#### ۱۸.۳.۱. تعریف `enum Command`
اول یک `enum` برای انواع دستورات ممکن تعریف می‌کنیم:
```rust
enum Command {
    Go { direction: String },
    Attack { target: String, power: u32 },
    Quit,
}
```

#### ۱۸.۳.۲. تابع `parse_command`
یک تابع می‌نویسیم که رشته‌ی ورودی را تجزیه کند و یک `Command` برگرداند. ورودی را با فاصله (`whitespace`) تکه‌تکه می‌کنیم. همچنین اگر ورودی خالی بود یا فرمت اشتباه داشت، دستور `Quit` در نظر گرفته می‌شود.
```rust
fn parse_command(input: &str) -> Command {
    let parts: Vec<&str> = input.trim().split_whitespace().collect();
    
    // اگر کاربر هیچ چیزی وارد نکرده باشد
    if parts.is_empty() {
        return Command::Quit;
    }
    
    // اگر کاربر "/go north" نوشته باشد
    if parts[0] == "/go" && parts.len() >= 2 {
        Command::Go {
            direction: parts[1].to_string(),
        }
    } 
    // اگر کاربر "/attack dragon 50" نوشته باشد
    else if parts[0] == "/attack" && parts.len() >= 3 {
        let power = parts[2].parse().unwrap_or(10); // اگر عدد نبود، ۱۰ در نظر بگیر
        Command::Attack {
            target: parts[1].to_string(),
            power,
        }
    } 
    // اگر "/quit" یا هر چیز دیگری باشد
    else {
        Command::Quit
    }
}
```

#### ۱۸.۳.۳. اجرای دستور با `match` و `guard`
حالا در `main` یک حلقه می‌گذاریم که دستورات را بگیرد و اجرا کند. از `match` با `guard` استفاده می‌کنیم تا برای حمله‌های خیلی قوی پیام مخصوص نشان بدهد:
```rust
use std::io;
use std::io::Write; // برای flush

fn main() {
    println!("🎮 به بازی متنی فریس خوش آمدی!");
    loop {
        print!("\nفرمان خودت را بنویس (/go, /attack, /quit): ");
        io::stdout().flush().unwrap(); // مطمئن می‌شویم پیام سریع چاپ شود
        
        let mut input = String::new();
        io::stdin().read_line(&mut input).unwrap();
        let cmd = parse_command(&input);

        match cmd {
            Command::Go { direction } => {
                println!("🚀 فریس به سمت {} حرکت کرد.", direction);
            }
            Command::Attack { target, power } if power > 30 => {
                println!("💥 حمله‌ی ویرانگر! {} با قدرت {} پودر شد!", target, power);
            }
            Command::Attack { target, power } => {
                println!("⚔️ حمله به {} با قدرت {}. (هنوز زنده است!)", target, power);
            }
            Command::Quit => {
                println!("👋 خداحافظ! بازی تمام شد.");
                break;
            }
        }
    }
}
```
ببین چقدر تمیز شد! دیگر نیازی به `if/else` تو در تو نیست. `match` همه‌چیز را مثل یک نقشه‌ی گنج باز می‌کند. 🗝️

![[Illustration: A retro computer terminal screen showing text commands: "/go north", "/attack dragon 50", "/quit". Next to the screen, a cartoon joystick with buttons labeled "Match", "Guard", "Enum". Ferris sits at the keyboard wearing a gaming headset, smiling confidently. Style: cozy gaming setup, vibrant, children's book illustration, 16:9.]](../assets/images/18.3.png)

---

### ۱۸.۴. جمع‌بندی و چالش

#### ۱۸.۴.۱. مرور مفاهیم
در این فصل یاد گرفتی:
✅ **تخریب (Destructuring)**: بیرون کشیدن فیلدهای `struct`، `enum` و `tuple` با الگو.  
✅ `_` و `..`: نادیده گرفتن بخش‌هایی از الگو وقتی بهشان نیاز نداری.  
✅ **Match Guard**: اضافه کردن شرط `if` به بازوی `match`.  
✅ `@` Binding: ذخیره‌ی مقدار جور شده در یک متغیر حین بررسی الگو.  
✅ `|`: ترکیب چند الگو در یک بازو برای جلوگیری از تکرار.  
✅ **این ابزارها تو را به یک کارآگاه داده تبدیل می‌کنند – یک جادوگر کامپیوتر واقعی!** 🧙

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> تخریب‌های تودرتو و match guard ممکن است در ابتدا کمی پیچیده به نظر برسند. نگران نباش – هر چه بیشتر از آن‌ها در کدهات استفاده کنی، طبیعی‌تر می‌شوند. حتی برنامه‌نویسان حرفه‌ای هم گاهی برای نوشتن یک الگوی پیچیده چند بار تلاش می‌کنند. مهم این است که بدانی Rust همیشه به تو می‌گوید کجا اشتباه کرده‌ای.

#### ۱۸.۴.۲. چالش: استخراج از `Option<Vec<i32>>`
یک تابع به اسم `sum_first_two` بنویس که یک `Option<Vec<i32>>` به عنوان ورودی بگیرد و:
- اگر `Some` بود و وکتور حداقل ۳ عنصر داشت، مجموع دو عنصر اول را به صورت `Some(i32)` برگرداند.
- اگر `Some` بود ولی کمتر از ۳ عنصر داشت، `None` برگرداند.
- اگر `None` بود، `None` برگرداند.

💡 **راهنمایی:** می‌توانی از یک `match` تودرتو یا یک `match guard` استفاده کنی.

💡 **پاسخ نمونه:**
```rust
fn sum_first_two(opt: Option<Vec<i32>>) -> Option<i32> {
    match opt {
        Some(vec) if vec.len() >= 3 => Some(vec[0] + vec[1]),
        _ => None, // هم Some با طول کم و هم None را پوشش می‌دهد
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

🔚 **پایان فصل ۱۸**

حالا تو یک استاد الگویابی شده‌ای و می‌توانی پیچیده‌ترین ساختارهای داده را مثل آب خوردن باز کنی و از آنها استفاده کنی. 🧩✨  
در فصل بعد، سری به اتاق موتور Rust می‌زنیم و با `unsafe` و ماکروها آشنا می‌شویم – ابزارهایی که فقط قهرمان‌های حرفه‌ای و ماجراجو از آنها استفاده می‌کنند! آماده‌ای برویم سراغ جادوی سیاه (ولی امن) برنامه‌نویسی؟ 🌙🔧

![[Illustration: Ferris wearing a graduation cap and holding a glowing "Chapter 18 Master" badge. Floating around him are nested puzzle boxes, match guard shields, and a joystick controller. Background: a starry night sky with a subtle map overlay. Encouraging, vibrant children's book style, 16:9.]](../assets/images/18.4.png)
