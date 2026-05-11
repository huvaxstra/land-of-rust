# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۷: کتابخانه‌ی بزرگ شهر (ماژول‌ها و فایل‌ها)

### 📑 فهرست فصل
[۷.۱. کتابخانه خیلی شلوغ شد!](#۷۱-کتابخانه-خیلی-شلوغ-شد)  
[۷.۱.۱. داستان: کتابخانه‌ی بی‌نظم فریس](#۷۱۱-داستان-کتابخانهی-بینظم-فریس)  
[۷.۱.۲. مشکل: همه چیز در یک فایل](#۷۱۲-مشکل-همه-چیز-در-یک-فایل)  
[۷.۱.۳. معرفی ماژول به عنوان قفسه](#۷۱۳-معرفی-ماژول-به-عنوان-قفسه)  
[۷.۲. قفسه‌بندی (mod)](#۷۲-قفسه‌بندی-mod)  
[۷.۲.۱. تعریف ماژول در یک فایل](#۷۲۱-تعریف-ماژول-در-یک-فایل)  
[۷.۲.۲. صدا زدن توابع ماژول](#۷۲۲-صدا-زدن-توابع-ماژول)  
[۷.۲.۳. ماژول‌های تو در تو](#۷۲۳-ماژول‌های-تو-در-تو)  
[۷.۲.۴. جدا کردن ماژول به فایل جداگانه](#۷۲۴-جدا-کردن-ماژول-به-فایل-جداگانه)  
[۷.۲.۵. تمرین: ماژول‌های ریاضی](#۷۲۵-تمرین-ماژول‌های-ریاضی)  
[۷.۳. قفل کتابخانه (Privacy)](#۷۳-قفل-کتابخانه-privacy)  
[۷.۳.۱. خصوصی بودن پیش‌فرض](#۷۳۱-خصوصی-بودن-پیش‌فرض)  
[۷.۳.۲. عمومی کردن با pub](#۷۳۲-عمومی-کردن-با-pub)  
[۷.۳.۳. فیلدهای خصوصی در struct](#۷۳۳-فیلدهای-خصوصی-در-struct)  
[۷.۳.۴. چرا محرمانگی مهم است؟](#۷۳۴-چرا-محرمانگی-مهم-است)  
[۷.۳.۵. تمرین: ماژول بانک](#۷۳۵-تمرین-ماژول-بانک)  
[۷.۴. میان‌برهای کتابخانه (use و as)](#۷۴-میان‌برهای-کتابخانه-use-و-as)  
[۷.۴.۱. آوردن توابع با use](#۷۴۱-آوردن-توابع-با-use)  
[۷.۴.۲. تغییر نام با as](#۷۴۲-تغییر-نام-با-as)  
[۷.۵. پروژه: بازسازی بازی حدس عدد با ماژول‌ها](#۷۵-پروژه-بازسازی-بازی-حدس-عدد-با-ماژول‌ها)  
[۷.۵.۱. ساختار پروژه](#۷۵۱-ساختار-پروژه)  
[۷.۵.۲. ماژول input](#۷۵۲-ماژول-input)  
[۷.۵.۳. ماژول random](#۷۵۳-ماژول-random)  
[۷.۵.۴. ماژول game_logic](#۷۵۴-ماژول-game_logic)  
[۷.۵.۵. فایل main.rs](#۷۵۵-فایل-mainrs)  
[۷.۶. جمع‌بندی و چالش](#۷۶-جمع‌بندی-و-چالش)  
[۷.۶.۱. مرور مفاهیم](#۷۶۱-مرور-مفاهیم)  
[۷.۶.۲. چالش: crate shapes](#۷۶۲-چالش-crate-shapes)  

---

### ۷.۱. کتابخانه خیلی شلوغ شد!

#### ۷.۱.۱. داستان: کتابخانه‌ی بی‌نظم فریس
فریس عاشق کتاب خواندن است و یک کتابخانه‌ی بزرگ در سفینه‌اش دارد. روزهای اول، همه‌ی کتاب‌ها را یکجا روی یک میز بزرگ می‌ریخت. 📚📖  
اما خیلی زود، تعداد کتاب‌ها زیاد شد و کتابخانه شبیه انبار آشغال شد! هر وقت می‌خواست «دانشنامه‌ی کهکشان‌ها» را پیدا کند، باید ساعت‌ها دنبال یک تکه کاغذ می‌گشت.  
بالاخره فریس تصمیم گرفت کتابخانه را مرتب کند. قفسه‌های جداگانه ساخت: یک قفسه برای کتاب‌های علمی، یکی برای داستان‌ها، یکی برای نقشه‌های ستاره‌ای و یکی هم برای کتاب‌های آشپزی فضایی! حالا همه‌چی سر جای خودش است و پیدا کردنشان آب خوردن است! 💧

#### ۷.۱.۲. مشکل: همه چیز در یک فایل
در برنامه‌نویسی هم دقیقاً همین اتفاق می‌افتد. تا اینجا ما همه‌ی کدهایمان را در یک فایل به اسم `main.rs` می‌نوشتیم. برای بازی حدس عدد (که حدود ۵۰ خط کد داشت) این کار عالی بود.  
اما تصور کن داری یک بازی بزرگ مثل «ماینکرفت» را می‌نویسی! هزاران خط کد، هزاران تابع و صدها متغیر! اگر همه را در یک فایل بریزی، پیدا کردن یک خط کوچک می‌شود مثل پیدا کردن یک سوزن در انبار کاه! 😵‍💫  
علاوه بر این، اگر چند نفر بخواهند با هم کار کنند، همه‌شان باید همان یک فایل را تغییر دهند و کلی هم دعوا می‌شود!

#### ۷.۱.۳. معرفی ماژول به عنوان قفسه
در Rust، راه حل این مشکل استفاده از **ماژول (Module)** است.  
ماژول مثل یک قفسه‌ی جداگانه است. هر قفسه می‌تواند کتاب‌های (کدهای) مخصوص خودش را داشته باشد.  
ماژول‌ها سه کار بزرگ برایمان می‌کنند:  
🔹 **سازماندهی**: کد را دسته‌بندی می‌کنند تا قشنگ و مرتب باشد.  
🔹 **محرمانگی**: می‌توانیم بعضی کدها را خصوصی نگه داریم تا کسی از بیرون دستکاریشان نکند.  
🔹 **جلوگیری از تداخل**: دو تا ماژول مختلف می‌توانند یک تابع به اسم یکسان داشته باشند بدون اینکه قاطی شوند!  

**این یعنی تو داری یک مهارت حرفه‌ای مهندسی نرم‌افزار را یاد می‌گیری – مدیر یک کتابخانه‌ی عظیم از کدها! هر قدمت به «جادوگر کامپیوتر» شدن نزدیک‌تر می‌کند.** 🧙‍♂️

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> ماژول‌ها روش Rust برای مدیریت کد در مقیاس بزرگ هستند. این مفهوم در تمام زبان‌های برنامه‌نویسی وجود دارد. این فصل نشان می‌دهد چطور از یک اسکریپت تک‌فایلی به یک پروژهٔ چندفایلی برویم – یک مهارت ضروری در دنیای واقعی. کتاب رسمی Rust فصل کاملی درباره‌ی ماژول‌ها دارد:  
> [doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html)

![[Illustration: Educational illustration of Ferris the crab standing in a messy spaceship room full of scattered books. On the right side, a clean, organized bookshelf with labeled shelves (Science, Stories, Maps) is shown. Ferris is happily placing a book on the correct shelf. Style: vibrant children's book, clean lines, soft lighting, 16:9.]](../assets/images/7.1.png)

---

### ۷.۲. قفسه‌بندی (mod)

#### ۷.۲.۱. تعریف ماژول در یک فایل
ساده‌ترین راه برای ساختن قفسه (ماژول)، استفاده از کلمه‌ی کلیدی `mod` است.  
می‌توانیم ماژول را همان در فایل `main.rs` تعریف کنیم:

```rust
mod animals {
    pub fn bark() {
        println!("هاپ! هاپ!");
    }

    pub struct Dog {
        pub name: String,
    }
}

fn main() {
    // استفاده از تابع داخل ماژول
    animals::bark(); 
    
    // ساختن یک سگ
    let my_dog = animals::Dog {
        name: String::from("رکسی"),
    };
    println!("اسم سگ من: {}", my_dog.name);
}
```

به کلمه‌ی `pub` (مخفف Public به معنی عمومی) دقت کن. هر چیزی که بخواهیم از بیرون ماژول صدایش بزنیم، باید `pub` باشد. در غیر این صورت، آن کد خصوصی می‌ماند و فقط داخل همان ماژول قابل استفاده است.

#### ۷.۲.۲. صدا زدن توابع ماژول
برای دسترسی به چیزی در یک ماژول، از علامت `::` (دو تا دونقطه) استفاده می‌کنیم.  
مثلاً `animals::bark()` یعنی: «برو به قفسه‌ی `animals` و تابع `bark` را پیدا کن و اجرایش کن!» 🐕

#### ۷.۲.۳. ماژول‌های تو در تو
می‌توانیم ماژول‌ها را مثل جعبه‌های تودرتو، داخل هم قرار دهیم:

```rust
mod house {
    pub mod kitchen {
        pub fn cook() {
            println!("آشپزی در آشپزخانه!");
        }
    }

    pub mod living_room {
        pub fn watch_tv() {
            println!("تماشای تلویزیون در پذیرایی!");
        }
    }
}

fn main() {
    house::kitchen::cook();
    house::living_room::watch_tv();
}
```

#### ۷.۲.۴. جدا کردن ماژول به فایل جداگانه
وقتی ماژول‌ها بزرگ می‌شوند، دیگر جای خوبی در `main.rs` ندارند. بهتر است هر کدام را ببریم در یک فایل جدا!  
برای این کار:
۱. یک فایل جدید کنار `main.rs` (در پوشه‌ی `src`) می‌سازیم با همان اسم ماژول و پسوند `.rs`.
۲. محتویات ماژول (بدون کلمه‌ی `mod`) را در آن فایل می‌نویسیم.
۳. در `main.rs` فقط می‌نویسیم: `mod animals;`

📂 **فایل `src/animals.rs`:**
```rust
pub fn bark() {
    println!("هاپ!");
}

pub struct Dog {
    pub name: String,
}
```

📂 **فایل `src/main.rs`:**
```rust
mod animals; // این خط به Rust می‌گوید فایل animals.rs را پیدا کن!

fn main() {
    animals::bark();
}
```
Rust خودش باهوش است و می‌فهمد که وقتی می‌نویسی `mod animals;` یعنی برو فایل `animals.rs` را بخوان. خیلی تمیز و مرتب! 🧹✨

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> استفاده از فایل‌های جداگانه ممکن است در ابتدا کمی عجیب به نظر برسد، اما بعد از چند بار تمرین برایت کاملاً طبیعی می‌شود. این دقیقاً همان روشی است که تمام پروژه‌های بزرگ Rust (حتی خود کامپایلر Rust) از آن استفاده می‌کنند.

#### ۷.۲.۵. تمرین: ماژول‌های ریاضی
یک پروژه جدید بساز (`cargo new math_modules`). دو تا ماژول به اسم‌های `math` و `strings` در فایل‌های جداگانه بساز.  
- ماژول `math`: تابع `add` و `subtract`.  
- ماژول `strings`: تابع `to_uppercase` و `to_lowercase`. (برای ساده‌تر شدن، می‌توانی از متدهای استاندارد `to_uppercase()` و `to_lowercase()` روی `String` استفاده کنی.)  
بعد در `main.rs` از همه‌شان استفاده کن.

![[Illustration: A cartoon carpenter Ferris building wooden shelves labeled "mod" and "pub". Each shelf holds different code blocks (functions, structs). Tools like a hammer and ruler are scattered around. Style: educational, playful, bright colors, children's book, 16:9.]](../assets/images/7.2.png)

---

### ۷.۳. قفل کتابخانه (Privacy)

#### ۷.۳.۱. خصوصی بودن پیش‌فرض
در Rust یک قانون طلایی داریم: **همه‌چی خصوصی است!** 🔒  
یعنی اگر یک تابع یا متغیر بسازی، فقط همان ماژول (و زیرماژول‌هایش) می‌توانند ببینندش.  
فکر کن یک دفترچه‌ی خاطرات داری. مگر می‌گذاری هر کسی بیاید بخواندش؟ نه! خودت تصمیم می‌گیری کدام صفحه‌ها را نشان بدهی.

#### ۷.۳.۲. عمومی کردن با pub
برای اینکه بقیه بتوانند یک چیز را ببینند، باید برچسب `pub` (عمومی) به آن بزنی:

```rust
mod my_module {
    pub fn public_function() {
        println!("همه می‌توانند من را ببینند!");
    }

    fn private_function() {
        println!("فقط اعضای این ماژول من را می‌بینند.");
    }
}
```

#### ۷.۳.۳. فیلدهای خصوصی در struct
حتی اگر یک `struct` عمومی باشد، فیلدهای داخلش (مثل `name` یا `power`) به‌طور پیش‌فرض خصوصی هستند!  
این خیلی خوب است چون اجازه می‌دهد ما کنترل کنیم چطور اطلاعات تغییر کنند. مثلاً در یک بازی، نباید کسی بتواند مستقیم `health` (سلامتی) قهرمان را زیاد کند؛ باید از تابع `heal()` استفاده کند که چک می‌کند آیا واقعاً دارو مصرف کرده یا نه.

#### ۷.۳.۴. چرا محرمانگی مهم است؟
🔹 **امنیت**: جلوی دسترسی غیرمجاز را می‌گیرد.  
🔹 **سادگی**: کاربر فقط با چیزهای لازم کار می‌کند و گیج نمی‌شود.  
🔹 **انعطاف**: می‌توانیم کدهای داخلی را تغییر دهیم بدون اینکه برنامه‌ی بقیه خراب شود (تا وقتی اسم توابع عمومی عوض نشود).

#### ۷.۳.۵. تمرین: ماژول بانک
یک ماژول `bank` بساز که یک حساب بانکی را مدیریت کند. یک `struct` به اسم `Account` داشته باشد که فیلد `balance` (موجودی) در آن خصوصی باشد.  
متدهای عمومی `deposit` (واریز) و `withdraw` (برداشت) بنویس. `withdraw` باید چک کند موجودی کافی هست یا نه و اگر بود کم کند.

💡 **راهنمایی ساده:**  
```rust
pub struct Account {
    balance: u32,
}

impl Account {
    pub fn new(initial_balance: u32) -> Account {
        Account { balance: initial_balance }
    }
    pub fn deposit(&mut self, amount: u32) {
        self.balance += amount;
    }
    pub fn withdraw(&mut self, amount: u32) -> bool {
        if amount <= self.balance {
            self.balance -= amount;
            true
        } else {
            false
        }
    }
    pub fn get_balance(&self) -> u32 {
        self.balance
    }
}
```

![[Illustration: Illustration of Ferris the crab standing in front of a bank vault door. One door is open with a bright "pub" sign, revealing shiny gold coins. The other door is closed with a heavy lock and a "private" sign. Style: educational cartoon, bright colors, clear metaphor, 16:9.]](../assets/images/7.3.png)

---

### ۷.۴. میان‌برهای کتابخانه (use و as)

گاهی نوشتن آدرس کامل (`animals::dog::bark()`) خیلی طولانی است!  
با کلمه‌ی `use` می‌توانیم یک چیز را بیاوریم در دسترس خودمان، درست مثل اینکه کتاب را از قفسه برداریم و بگذاریم روی میز کار.

#### ۷.۴.۱. آوردن توابع با use
```rust
mod animals {
    pub mod dog {
        pub fn bark() {
            println!("هاپ!");
        }
    }
}

use crate::animals::dog::bark;

fn main() {
    bark(); // دیگر لازم نیست آدرس کامل بنویسی!
}
```

#### ۷.۴.۲. تغییر نام با as
اگر دو تا تابع هم‌نام از دو ماژول مختلف داشته باشیم، با `use` قاطی می‌شوند!  
برای حل این مشکل، با `as` بهشان اسم مستعار می‌دهیم:

```rust
use animals::dog::bark as dog_bark;
use animals::cat::speak as cat_speak; // فرض کنیم گربه هم صدایی دارد
```

> 💡 **نکته:** `as` خیلی به کار می‌آید وقتی می‌خواهی اسم کوتاه‌تر یا معنی‌دارتری برای یک تابع بگذاری.

در این کتاب فعلاً همین دو کاربرد `use` کافی است. بعداً که بزرگتر شدی، روش‌های پیشرفته‌تری هم یاد می‌گیری (مثل nested paths). اما الان همین قدر بدان که `use` دستت را برای نوشتن کدهای تمیز باز می‌گذارد. 

![[Illustration: A cartoon map showing a path from "crate" root to a function. A magnifying glass focuses on a shortcut sign labeled "use". Ferris is walking a shorter path thanks to the shortcut. Style: playful vector illustration, clear educational graphic, 16:9.]](../assets/images/7.4.png)

---

### ۷.۵. پروژه: بازسازی بازی حدس عدد با ماژول‌ها

حالا وقتش است بازی حدس عدد (فصل ۲) را با استفاده از ماژول‌ها بازنویسی کنیم تا ببینیم چقدر تمیز و حرفه‌ای می‌شود!

#### ۷.۵.۱. ساختار پروژه
اول فایل‌ها را در پوشه‌ی `src` اینطوری می‌چینیم:
```
src/
├── main.rs
├── input.rs       // مسئول گرفتن ورودی از کاربر
├── random.rs      // مسئول ساخت عدد تصادفی
└── game_logic.rs  // مسئول مقایسه و منطق بازی
```
(یادت نرود در `Cargo.toml` وابستگی `rand` را اضافه کنی!)

#### ۷.۵.۲. ماژول input (`src/input.rs`)
این فایل فقط کارش این است که یک عدد تمیز از کاربر بگیرد. اگر کاربر اشتباه تایپ کرد، دوباره می‌پرسد.

```rust
use std::io;

pub fn read_number() -> u32 {
    loop {
        println!("لطفاً یک عدد حدس بزن:");
        let mut input = String::new();
        io::stdin().read_line(&mut input).expect("خطا");

        match input.trim().parse() {
            Ok(num) => return num,
            Err(_) => println!("فقط عدد وارد کن!"),
        }
    }
}
```

#### ۷.۵.۳. ماژول random (`src/random.rs`)
عدد مخفی را اینجا می‌سازیم.

```rust
use rand::Rng;

pub fn generate_secret() -> u32 {
    rand::thread_rng().gen_range(1..=100)
}
```

#### ۷.۵.۴. ماژول game_logic (`src/game_logic.rs`)
اینجا مقایسه می‌کنیم. یک `enum` هم می‌سازیم که وضعیت بازی را نگه دارد.

```rust
pub enum GuessResult {
    TooLow,
    TooHigh,
    Correct,
}

pub fn check_guess(guess: u32, secret: u32) -> GuessResult {
    if guess < secret { GuessResult::TooLow }
    else if guess > secret { GuessResult::TooHigh }
    else { GuessResult::Correct }
}

pub fn get_message(result: &GuessResult) -> &'static str {
    match result {
        GuessResult::TooLow => "⬆️ برو بالا!",
        GuessResult::TooHigh => "⬇️ بیا پایین!",
        GuessResult::Correct => "🏆 بردی!",
    }
}
```

#### ۷.۵.۵. فایل main.rs
حالا نگاه کن `main.rs` چقدر خلوت و خوانا شده است!

```rust
mod input;
mod random;
mod game_logic;

use game_logic::GuessResult;

fn main() {
    println!("🎲 به بازی حدس عدد خوش آمدید! 🎲");
    let secret = random::generate_secret();
    let mut count = 0;

    loop {
        let guess = input::read_number();
        count += 1;

        let result = game_logic::check_guess(guess, secret);
        println!("{}", game_logic::get_message(&result));

        if let GuessResult::Correct = result {
            println!("✨ تو در {} تا حدس بردی! ✨", count);
            break;
        }
    }
}
```
دیگر لازم نیست ۱۰۰ خط کد را در یک فایل بخوانی! هر بخش دارد کار خودش را می‌کند. 😎

![[Illustration: A cartoon folder tree structure showing src/ folder with four glowing files: main.rs, input.rs, random.rs, game_logic.rs. Arrows connect them showing how modules interact. Ferris stands beside giving a thumbs up. Style: clean infographic, educational, bright colors, 16:9.]](../assets/images/7.5.png)

---

### ۷.۶. جمع‌بندی و چالش

#### ۷.۶.۱. مرور مفاهیم
در این فصل یاد گرفتی:
✅ **ماژول‌ها (`mod`)**: کد را به بخش‌های کوچک و مرتب تقسیم می‌کنند.  
✅ **`pub`**: برای عمومی کردن توابع و متغیرها (در غیر این صورت خصوصی هستند).  
✅ **فایل‌ها**: ماژول‌ها می‌توانند در فایل‌های `.rs` جداگانه باشند.  
✅ **`use`**: برای کوتاه کردن مسیر دسترسی به آیتم‌ها.  
✅ **`as`**: برای تغییر نام یک تابع یا نوع هنگام `use` کردن.

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> استفاده از ماژول‌ها و فایل‌های جداگانه ممکن است در ابتدا کار اضافی به نظر برسد، اما به محض اینکه پروژه‌ات رشد کند، می‌بینی که چقدر این روش به تو کمک می‌کند تا کدهای خود را سازماندهی کنی. مثل این است که اتاقت را مرتب کنی – اولش سخت است، اما بعداً خیلی راحت‌تر می‌توانی وسایلت را پیدا کنی.

#### ۷.۶.۲. چالش: crate shapes
یک پروژه‌ی جدید به اسم `shapes` بساز.  
دو تا ماژول `circle` و `rectangle` در فایل‌های جدا بساز.  
هر کدام باید دو تابع داشته باشند: `area` (مساحت) و `perimeter` (محیط).  
- دایره: شعاع `r`. (فرمول مساحت: π × r²)  
- مستطیل: طول `a` و عرض `b`.  

در `main.rs` این توابع را صدا بزن و نتیجه را برای یک دایره با شعاع ۵ و مستطیل ۴×۷ چاپ کن.

💡 **پاسخ نمونه (`circle.rs`):**
```rust
pub fn area(radius: f64) -> f64 {
    std::f64::consts::PI * radius * radius
}

pub fn perimeter(radius: f64) -> f64 {
    2.0 * std::f64::consts::PI * radius
}
```

حالا تو یک برنامه‌نویس واقعی شده‌ای که می‌داند چطور پروژه‌های بزرگ را مدیریت کند! 🏗️  
در فصل بعد با **Collections (وکتورها و هش‌مپ‌ها)** آشنا می‌شویم؛ جعبه‌های جادویی که می‌توانند بزرگ و کوچک شوند و کلی داده را در خودشان نگه دارند. 📦✨

![[Illustration: Ferris the crab wearing a graduation cap, holding a glowing badge "Chapter 7 Master". Background shows a well-organized file cabinet with labels "mod", "pub", "use". Floating icons of Rust files and folders surround him. Style: encouraging, vibrant children's book, 16:9.]](../assets/images/7.6.png)
