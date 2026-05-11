# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۱۴: سوپرمارکت اسباب‌بازی‌های راست (Crates.io)

### 📑 فهرست فصل
[۱۴.۱. قرض گرفتن اسباب‌بازی بقیه](#۱۴۱-قرض-گرفتن-اسباب‌بازی-بقیه)  
[۱۴.۱.۱. داستان: فروشگاه بزرگ اسباب‌بازی](#۱۴۱۱-داستان-فروشگاه-بزرگ-اسباب‌بازی)  
[۱۴.۱.۲. crates.io چیست؟](#۱۴۱۲-cratesio-چیست)  
[۱۴.۱.۳. اضافه کردن وابستگی به Cargo.toml](#۱۴۱۳-اضافه-کردن-وابستگی-به-cargotoml)  
[۱۴.۱.۴. استفاده از crate در کد](#۱۴۱۴-استفاده-از-crate-در-کد)  
[۱۴.۲. جستجو و انتخاب crate](#۱۴۲-جستجو-و-انتخاب-crate)  
[۱۴.۲.۱. رفتن به سایت crates.io](#۱۴۲۱-رفتن-به-سایت-cratesio)  
[۱۴.۲.۲. خواندن مستندات در docs.rs](#۱۴۲۲-خواندن-مستندات-در-docsrs)  
[۱۴.۲.۳. معیارهای انتخاب یک crate خوب](#۱۴۲۳-معیارهای-انتخاب-یک-crate-خوب)  
[۱۴.۲.۴. مثال: استفاده از rand](#۱۴۲۴-مثال-استفاده-از-rand)  
[۱۴.۳. مدیریت نسخه‌ها (SemVer)](#۱۴۳-مدیریت-نسخه‌ها-semver)  
[۱۴.۳.۱. معناشناسی نسخه (Semantic Versioning)](#۱۴۳۱-معناشناسی-نسخه-semantic-versioning)  
[۱۴.۳.۲. انواع عملگرهای نسخه در Cargo.toml](#۱۴۳۲-انواع-عملگرهای-نسخه-در-cargotoml)  
[۱۴.۳.۳. قفل کردن نسخه با Cargo.lock](#۱۴۳۳-قفل-کردن-نسخه-با-cargolock)  
[۱۴.۴. به‌روزرسانی وابستگی‌ها](#۱۴۴-به‌روزرسانی-وابستگی‌ها)  
[۱۴.۴.۱. cargo update](#۱۴۴۱-cargo-update)  
[۱۴.۴.۲. cargo outdated (ابزار خارجی)](#۱۴۴۲-cargo-outdated-ابزار-خارجی)  
[۱۴.۵. ساختن اولین crate خودمان](#۱۴۵-ساختن-اولین-crate-خودمان)  
[۱۴.۵.۱. ایجاد پروژه کتابخانه](#۱۴۵۱-ایجاد-پروژه-کتابخانه)  
[۱۴.۵.۲. نوشتن کد در lib.rs](#۱۴۵۲-نوشتن-کد-در-librs)  
[۱۴.۵.۳. مستندات با /// و //!](#۱۴۵۳-مستندات-با-و-)  
[۱۴.۵.۴. ساختن مستندات محلی با cargo doc](#۱۴۵۴-ساختن-مستندات-محلی-با-cargo-doc)  
[۱۴.۵.۵. آماده کردن برای انتشار (اختیاری)](#۱۴۵۵-آماده-کردن-برای-انتشار-اختیاری)  
[۱۴.۶. پروژه: استفاده از ferris-says](#۱۴۶-پروژه-استفاده-از-ferris-says)  
[۱۴.۶.۱. اضافه کردن ferris-says](#۱۴۶۱-اضافه-کردن-ferris-says)  
[۱۴.۶.۲. نوشتن برنامه با فریم خرچنگ](#۱۴۶۲-نوشتن-برنامه-با-فریم-خرچنگ)  
[۱۴.۷. جمع‌بندی و چالش](#۱۴۷-جمع‌بندی-و-چالش)  
[۱۴.۷.۱. مرور مفاهیم](#۱۴۷۱-مرور-مفاهیم)  
[۱۴.۷.۲. چالش: ساختن یک crate کوچک به نام pig_latin](#۱۴۷۲-چالش-ساختن-یک-crate-کوچک-به-نام-pig_latin)  

---

### ۱۴.۱. قرض گرفتن اسباب‌بازی بقیه

#### ۱۴.۱.۱. داستان: فروشگاه بزرگ اسباب‌بازی
فریس یک روز خسته شد از اینکه برای هر کار کوچکی (مثل ساختن عدد تصادفی یا کشیدن یک شکل ساده) مجبور بود همه‌چیز را از صفر بنویسد. دوستش بیل به او گفت: «چرا به فروشگاه بزرگ اسباب‌بازی‌های برنامه‌نویسی نمی‌روی؟ آنجا پر از ابزارهای آماده است که بقیه ساخته‌اند و رایگان گذاشته‌اند. می‌توانی آن‌ها را قرض بگیری و کارت را سریع‌تر راه بیندازی!» 🛍️✨  
در دنیای Rust به این فروشگاه می‌گویند **crates.io**. هر کدام از آن ابزارهای آماده هم یک **Crate** (جعبه/بسته) نامیده می‌شوند.  

**یادگیری استفاده از کتابخانه‌های دیگران یعنی می‌توانی روی شانه‌های غول‌ها بایستی و نرم‌افزارهای بزرگ‌تر بسازی – این قدرت یک جادوگر کامپیوتر است!** 🧙‍♂️

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> crates.io مخزن رسمی کتابخانه‌های Rust است. این فصل نحوه استفاده از وابستگی‌ها و مدیریت نسخه را نشان می‌دهد – مهارتی ضروری در دنیای واقعی. کتاب رسمی Rust فصل کاملی درباره‌ی crates.io دارد:  
> [doc.rust-lang.org/book/ch14-00-more-about-cargo.html](https://doc.rust-lang.org/book/ch14-00-more-about-cargo.html)

#### ۱۴.۱.۲. crates.io چیست؟
[crates.io](https://crates.io) یک سایت بزرگ است که برنامه‌نویس‌های سراسر دنیا کدهایشان را آنجا می‌گذارند تا بقیه از آن استفاده کنند. کارگو (Cargo) هم مثل یک دستیار هوشمند، وقتی بهش بگویی چه ابزاری می‌خواهی، خودش می‌رود آنجا، دانلودش می‌کند و می‌چسباند به پروژه‌ات. دیگر لازم نیست خودت فایل‌ها را کپی‌پیست کنی! 📦🤖

#### ۱۴.۱.۳. اضافه کردن وابستگی به Cargo.toml
برای قرض گرفتن یک Crate، باید اسمش را در فایل `Cargo.toml` بنویسی. مثلاً اگر بخواهیم از `rand` (که قبلاً یاد گرفتیم) استفاده کنیم، فایل `Cargo.toml` را باز می‌کنیم و زیر بخش `[dependencies]` می‌نویسیم:
```toml
[dependencies]
rand = "0.9.0"
```
حالا اگر `cargo build` بزنی، کارگو خودش می‌رود به crates.io، نسخه‌ی `0.9.0` را دانلود می‌کند و آماده‌ی استفاده می‌شود.

#### ۱۴.۱.۴. استفاده از crate در کد
حالا در `main.rs` می‌توانیم از آن استفاده کنیم:
```rust
use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    let secret_number = rng.gen_range(1..=100);
    println!("عدد مخفی: {}", secret_number);
}
```
💡 خط `use rand::Rng;` خیلی مهم است! این خط به Rust می‌گوید: «لطفاً دستورالعمل‌های ساخت عدد تصادفی را هم بیاور.» اگر این خط را ننویسی، کامپایلر `gen_range` را نمی‌شناسد.

![[Illustration: Cartoon illustration of a friendly crab (Ferris) pushing a shopping cart in a giant digital supermarket. The shelves are filled with glowing boxes labeled with crate names like "rand", "serde", "tokio". A friendly cargo robot scans a box and adds it to the cart. Style: vibrant children's book, playful tech metaphor, soft lighting, 16:9.]](../assets/images/14.1.png)

---

### ۱۴.۲. جستجو و انتخاب crate

#### ۱۴.۲.۱. رفتن به سایت crates.io
مرورگرت را باز کن و برو به [crates.io](https://crates.io). در نوار جستجو هر چیزی که می‌خواهی را بنویس (مثلاً `json` یا `image`). لیستی از Crateها می‌آید.

#### ۱۴.۲.۲. خواندن مستندات در docs.rs
هر Crate یک لینک به **مستندات (Docs)** دارد که معمولاً به آدرس `https://docs.rs/اسم-crate` می‌رود. آنجا مثل دفترچه‌ی راهنمای یک اسباب‌بازی است: توضیح می‌دهد چطور نصبش کنی، چه توابعی دارد و مثال‌های آماده دارد. همیشه قبل از استفاده، یک نگاه به docs.rs بینداز! 📖

#### ۱۴.۲.۳. معیارهای انتخاب یک crate خوب
چون هر کسی می‌تواند Crate منتشر کند، بعضی‌هایشان بهترند. به این چند تا چیز دقت کن:
🔹 **تعداد دانلودها:** هرچی بیشتر باشد، یعنی آدم‌های بیشتری از آن راضی‌اند.  
🔹 **آخرین آپدیت:** اگر سال‌هاست آپدیت نشده، ممکن است با نسخه‌های جدید Rust سازگار نباشد.  
🔹 **مستندات کامل:** آیا مثال ساده دارد؟ آیا توابع توضیح داده شده‌اند؟  
🔹 **لایسنس (مجوز):** مطمئن شو مجوزش آزاد است (مثل `MIT` یا `Apache-2.0`).

#### ۱۴.۲.۴. مثال: استفاده از rand
بیا یک مثال دیگر بزنیم: ساختن یک رنگ تصادفی RGB:
```rust
use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    let red = rng.gen_range(0..=255);
    let green = rng.gen_range(0..=255);
    let blue = rng.gen_range(0..=255);
    println!("رنگ تصادفی: rgb({}, {}, {})", red, green, blue);
}
```
هر بار اجرا کنی، یک رنگ جدید می‌بینی! 🎨

![[Illustration: A cartoon computer screen showing the docs.rs website for the "rand" crate. A magnifying glass hovers over a "Examples" section. Ferris stands beside taking notes with a pencil. Style: clean educational vector, bright colors, clear UI focus, 16:9.]](../assets/images/14.2.png)

---

### ۱۴.۳. مدیریت نسخه‌ها (SemVer)

#### ۱۴.۳.۱. معناشناسی نسخه (Semantic Versioning)
شماره‌ی نسخه‌ها در Rust سه قسمت دارد: `MAJOR.MINOR.PATCH` (مثلاً `1.2.3`). این یک قرارداد جهانی است:
🔸 **MAJOR (اصلی):** وقتی عدد اول عوض می‌شود، یعنی تغییرات بزرگ و ناسازگار داده شده. (مثل بازی v1 که قوانینش با v2 کاملاً فرق می‌کند).  
🔸 **MINOR (فرعی):** وقتی عدد وسط عوض می‌شود، یعنی قابلیت جدید اضافه شده ولی کدهای قبلی همچنان کار می‌کنند.  
🔸 **PATCH (وصله):** وقتی عدد آخر عوض می‌شود، یعنی فقط باگ‌ها رفع شده‌اند و هیچ چیزی خراب نمی‌شود. 🐛➡️✅

#### ۱۴.۳.۲. انواع عملگرهای نسخه در Cargo.toml
در `Cargo.toml` می‌توانی دقیق‌تر بگویی چه نسخه‌هایی را قبول داری:

| نوشتن در TOML | معنی |
|--------------|------|
| `"0.9.0"` | دقیقاً نسخه‌ی 0.9.0 (یا معادل `^0.9.0`) |
| `"^0.9.0"` | هر نسخه‌ای که **سازگار** باشد (یعنی `0.9.x` که `x >= 0`). حالت پیش‌فرض کارگو همین است. |
| `"~0.9.0"` | فقط `0.9.x` (اجازه تغییر MINOR را نمی‌دهد). |
| `"*"` | هر نسخه‌ای! (توصیه نمی‌شود چون ممکن است یکهو برنامه‌ات خراب شود). |

💡 برای شروع، همان `"0.9.0"` یا `"0.9"` کافی و امن است.

#### ۱۴.۳.۳. قفل کردن نسخه با Cargo.lock
وقتی اولین بار `cargo build` را می‌زنی، کارگو یک فایل به اسم `Cargo.lock` می‌سازد. این فایل دقیقاً یادداشت می‌کند که امروز چه نسخه‌ای از هر Crate نصب شد.  
اگر پروژه‌ات را به دوستت بدهی، او هم `Cargo.lock` را داشته باشد، دقیقاً همان نسخه‌هایی را نصب می‌کند که تو نصب کردی. این‌طوری برنامه‌ی هیچ‌کس بدون دلیل خراب نمی‌شود! 🔒📝

![[Illustration: A cartoon receipt labeled "Cargo.lock" with exact version numbers listed (rand = 0.9.0, ferris-says = 0.3.0). A friendly robot stamps it "LOCKED". Ferris holds the receipt next to a shopping bag. Style: playful metaphor, educational, soft lighting, 16:9.]](../assets/images/14.3.png)

---

### ۱۴.۴. به‌روزرسانی وابستگی‌ها

#### ۱۴.۴.۱. cargo update
بعد از یک مدت، ممکن است Crateهایی که استفاده می‌کنی آپدیت شوند. برای اینکه کارگو برود و نسخه‌های جدیدترِ **سازگار** را چک و نصب کند، بزن:
```bash
cargo update
```
این دستور `Cargo.lock` را آپدیت می‌کند، ولی `Cargo.toml` را دست نمی‌زند.

#### ۱۴.۴.۲. cargo outdated (ابزار خارجی)
اگر کنجکاو باشی بدانی کدام Crateها نسخه‌ی اصلی (Major) جدید دارند، می‌توانی یک ابزار کمکی نصب کنی:
```bash
cargo install cargo-outdated
cargo outdated
```
یک جدول خوشگل به تو نشان می‌دهد که کدام‌ها قدیمی شده‌اند. 📊

![[Illustration: A cartoon terminal window showing a colorful table with crate names, current versions, and newer available versions. Ferris points to a row with an upward arrow indicating an update. Style: modern tech illustration, clear and bright, 16:9.]](../assets/images/14.4.png)

---

### ۱۴.۵. ساختن اولین crate خودمان

#### ۱۴.۵.۱. ایجاد پروژه کتابخانه
حالا که قرض گرفتن را یاد گرفتیم، چرا خودمان یک ابزار نسازیم؟ یک پروژه‌ی **کتابخانه‌ای** (نه برنامه‌ی اجرایی) می‌سازیم:
```bash
cargo new my_math --lib
cd my_math
```
کارگو این بار به جای `main.rs` یک فایل `src/lib.rs` می‌سازد. اینجا نقطه‌ی شروع کتابخانه‌ی تو است! 📚

#### ۱۴.۵.۲. نوشتن کد در lib.rs
در `lib.rs` چند تابع ساده می‌نویسیم:
```rust
//! این یک کتابخانه‌ی ساده برای عملیات ریاضی است.

/// دو عدد صحیح را با هم جمع می‌کند.
///
/// # مثال
///
/// ```
/// let result = my_math::add(2, 3);
/// assert_eq!(result, 5);
/// ```
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}

/// دو عدد صحیح را از هم کم می‌کند.
pub fn subtract(a: i32, b: i32) -> i32 {
    a - b
}
```

#### ۱۴.۵.۳. مستندات با `///` و `//!`
🔹 `//!` در ابتدای فایل: برای توضیح کل کتابخانه است.  
🔹 `///` قبل از تابع/struct: برای توضیح همان آیتم خاص است.  
💡 متن داخل `///` می‌تواند Markdown باشد. کدهای داخل بلوک ````rust حتی توسط `cargo test` اجرا می‌شوند تا مطمئن شویم مثال‌هایمان همیشه درست کار می‌کنند!

#### ۱۴.۵.۴. ساختن مستندات محلی با cargo doc
برای دیدن مستنداتت در مرورگر، فقط کافی است بزنی:
```bash
cargo doc --open
```
یک صفحه‌ی حرفه‌ای شبیه docs.rs باز می‌شود که توضیحات خودت در آن است! ببین چقدر قشنگ شده؟ 🌟

#### ۱۴.۵.۵. آماده کردن برای انتشار (اختیاری)
اگر روزی خواستی کتابخانه‌ات را بگذاری روی crates.io تا همه استفاده کنند:
۱. در [crates.io](https://crates.io) حساب بساز و یک توکن بگیر.  
۲. در ترمینال `cargo login` بزن و توکن را بگذار.  
۳. مطمئن شو `Cargo.toml` اطلاعات لازم را دارد (`description`, `license`, `authors`).  
۴. دستور جادویی را بزن: `cargo publish` 🚀  
(البته برای تمرین لازم نیست واقعاً منتشر کنی!)

![[Illustration: A cozy desk setup with a laptop showing a beautiful documentation page generated by cargo doc. Floating around are markdown symbols, function signatures, and a glowing "cargo doc --open" badge. Ferris proudly holds a printed manual. Style: warm, educational children's book illustration, inviting atmosphere, 16:9.]](../assets/images/14.5.png)

---

### ۱۴.۶. پروژه: استفاده از ferris-says

#### ۱۴.۶.۱. اضافه کردن ferris-says
بیا یک Crate بامزه و سرگرم‌کننده را امتحان کنیم که تصویر فریس را با یک پیام چاپ می‌کند. در `Cargo.toml` یک پروژه‌ی جدید بنویس:
```toml
[dependencies]
ferris-says = "0.3"
```

#### ۱۴.۶.۲. نوشتن برنامه با فریم خرچنگ
کد زیر را در `main.rs` بنویس:
```rust
use ferris_says::say;
use std::io::{stdout, BufWriter};

fn main() {
    let message = String::from("سلام رفقا! من فریس هستم 🦀");
    let width = message.chars().count();

    let mut writer = BufWriter::new(stdout());
    say(&message, width, &mut writer).unwrap();
}
```
وقتی `cargo run` بزنی، خروجی چیزی شبیه این می‌شود:
```
 ____________________________
< سلام رفقا! من فریس هستم 🦀 >
 ----------------------------
        \
         \
            _~^~^~_
        \) /  o o  \ (/
          '_   -   _'
          / '-----' \
```
بامزه است، نه؟ حالا می‌توانی هر پیامی که دوست داری را جایگزین کنی! 🎤

![[Illustration: A cartoon terminal window displaying the exact ASCII art output of the ferris-says crate. Ferris the crab sits next to the screen waving, with speech bubbles containing the same message. Style: playful, tech-meets-art, bright and cheerful, 16:9.]](../assets/images/14.6.png)

---

### ۱۴.۷. جمع‌بندی و چالش

#### ۱۴.۷.۱. مرور مفاهیم
در این فصل یاد گرفتی:  
✅ **crates.io**: فروشگاه بزرگ کتابخانه‌های Rust.  
✅ **Cargo.toml**: جایی که وابستگی‌ها را می‌نویسیم (`[dependencies]`).  
✅ **SemVer**: قانون نسخه‌بندی `MAJOR.MINOR.PATCH`.  
✅ **Cargo.lock**: قفل کردن نسخه‌ها برای اطمینان از ساخت یکسان.  
✅ `cargo update` و `cargo outdated`: مدیریت به‌روزرسانی.  
✅ ساخت کتابخانه: با `cargo new --lib` و فایل `lib.rs`.  
✅ مستندات: با `///` و `cargo doc`.  
✅ **به اشتراک گذاشتن کد با دیگران یعنی تو بخشی از خانواده‌ی بزرگ Rust هستی – یک قدم بزرگ به سوی جادوگر کامپیوتر شدن!** 🧙

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> مدیریت وابستگی‌ها و انتخاب نسخه مناسب ممکن است در ابتدا کمی گیج‌کننده به نظر برسد. نگران نباش – کارگو بیشتر کارها را خودش انجام می‌دهد. با کمی تمرین، اضافه کردن یک crate جدید برایت مثل آب خوردن می‌شود.

#### ۱۴.۷.۲. چالش: ساختن یک crate کوچک به نام pig_latin
یک کتابخانه به اسم `pig_latin` بساز که یک تابع عمومی `to_pig_latin(word: &str) -> String` داشته باشد. این تابع یک کلمه‌ی انگلیسی را به زبان خوکی (Pig Latin) تبدیل کند:
🔸 اگر با حرف بی‌صدا شروع شود: حرف اول برود آخر و `"ay"` اضافه شود. (`"hello"` → `"ellohay"`)  
🔸 اگر با حرف صدادار (`a, e, i, o, u`) شروع شود: فقط `"hay"` به آخر اضافه شود. (`"apple"` → `"applehay"`)  

سپس یک پروژه‌ی اجرایی جداگانه بساز و این کتابخانه را به آن اضافه کن و چند کلمه را تست کن.
💡 **راهنمایی وابستگی محلی:** در `Cargo.toml` پروژه‌ی اجرایی بنویس:
```toml
[dependencies]
pig_latin = { path = "../pig_latin" }
```

💡 **پاسخ نمونه برای تابع:**
```rust
pub fn to_pig_latin(word: &str) -> String {
    let vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'];
    let mut chars = word.chars();
    
    if let Some(first_char) = chars.next() {
        if vowels.contains(&first_char) {
            format!("{}-hay", word)
        } else {
            format!("{}-{}ay", chars.as_str(), first_char)
        }
    } else {
        String::new()
    }
}
```

حالا تو هم می‌دانی چطور از کتابخانه‌های آماده استفاده کنی و هم می‌دانی چطور کتابخانه‌ی خودت را بسازی و با دیگران به اشتراک بگذاری. در فصل بعد، با **Smart Pointers** آشنا می‌شویم: ابزارهایی مثل `Box`، `Rc` و `RefCell` که به ما اجازه می‌دهند داده‌ها را هوشمندانه‌تر مدیریت کنیم. 📦🧠✨

![[Illustration: Ferris wearing a graduation cap and holding a glowing "Chapter 14 Master" badge. Floating around him are a shopping cart, a Cargo.lock receipt, a lib.rs file, and a documentation book. Encouraging, vibrant children's book illustration, celebratory mood, 16:9.]](../assets/images/14.7.png)
