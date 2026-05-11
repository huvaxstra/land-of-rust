# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۱۱: دکمه‌ی خود-تخریب را تست کن! (تست‌نویسی)

### 📑 فهرست فصل
[۱۱.۱. قبل از پرتاب سفینه: شبیه‌ساز](#۱۱۱-قبل-از-پرتاب-سفینه-شبیه‌ساز)  
[۱۱.۱.۱. داستان: شبیه‌ساز پرواز فریس](#۱۱۱۱-داستان-شبیه‌ساز-پرواز-فریس)  
[۱۱.۱.۲. تست چیست؟](#۱۱۱۲-تست-چیست)  
[۱۱.۱.۳. اولین تست با #[test]](#۱۱۱۳-اولین-تست-با-test)  
[۱۱.۱.۴. اجرای تست با cargo test](#۱۱۱۴-اجرای-تست-با-cargo-test)  
[۱۱.۱.۵. خواندن خروجی تست](#۱۱۱۵-خواندن-خروجی-تست)  
[۱۱.۲. ماکروهای پرکاربرد تست](#۱۱۲-ماکروهای-پرکاربرد-تست)  
[۱۱.۲.۱. assert!](#۱۱۲۱-assert)  
[۱۱.۲.۲. assert_eq! و assert_ne!](#۱۱۲۲-assert_eq-و-assert_ne)  
[۱۱.۲.۳. اضافه کردن پیام سفارشی](#۱۱۲۳-اضافه-کردن-پیام-سفارشی)  
[۱۱.۲.۴. should_panic](#۱۱۲۴-should_panic)  
[۱۱.۲.۵. تمرین: تست تابع add](#۱۱۲۵-تمرین-تست-تابع-add)  
[۱۱.۳. سازماندهی تست‌ها](#۱۱۳-سازماندهی-تست‌ها)  
[۱۱.۳.۱. تست‌های واحد (Unit Tests)](#۱۱۳۱-تست‌های-واحد-unit-tests)  
[۱۱.۳.۲. ماژول tests و #[cfg(test)]](#۱۱۳۲-ماژول-tests-و-cfgtest)  
[۱۱.۳.۳. تست‌های یکپارچه‌سازی (Integration Tests)](#۱۱۳۳-تست‌های-یکپارچه‌سازی-integration-tests)  
[۱۱.۳.۴. اجرای فقط یک تست](#۱۱۳۴-اجرای-فقط-یک-تست)  
[۱۱.۳.۵. نادیده گرفتن تست با ignore](#۱۱۳۵-نادیده-گرفتن-تست-با-ignore)  
[۱۱.۴. پروژه: تست برای بازی حدس عدد (فصل ۲)](#۱۱۴-پروژه-تست-برای-بازی-حدس-عدد-فصل-۲)  
[۱۱.۴.۱. تبدیل بازی به کتابخانه](#۱۱۴۱-تبدیل-بازی-به-کتابخانه)  
[۱۱.۴.۲. تابع generate_secret با دانه ثابت](#۱۱۴۲-تابع-generate_secret-با-دانه-ثابت)  
[۱۱.۴.۳. تابع check_guess](#۱۱۴۳-تابع-check_guess)  
[۱۱.۴.۴. نوشتن تست‌ها](#۱۱۴۴-نوشتن-تست‌ها)  
[۱۱.۴.۵. تست تابع read_input با شبیه‌سازی](#۱۱۴۵-تست-تابع-read_input-با-شبیه‌سازی)  
[۱۱.۵. جمع‌بندی و چالش](#۱۱۵-جمع‌بندی-و-چالش)  
[۱۱.۵.۱. مرور مفاهیم](#۱۱۵۱-مرور-مفاهیم)  
[۱۱.۵.۲. چالش: تست برای struct Monster](#۱۱۵۲-چالش-تست-برای-struct-monster)  

---

### ۱۱.۱. قبل از پرتاب سفینه: شبیه‌ساز

#### ۱۱.۱.۱. داستان: شبیه‌ساز پرواز فریس
فریس قبل از اینکه واقعاً دکمه‌ی پرتاب سفینه را بزند، همه‌ی سیستم‌ها را در یک اتاق شبیه‌ساز امتحان می‌کند. 🚀🕹️ دکمه‌ها را فشار می‌دهد، موتورها را روشن می‌کند، فرمان را می‌چرخاند و چک می‌کند آیا همه‌چیز درست کار می‌کند یا نه. اگر در شبیه‌ساز چراغی قرمز شود، فریس خوشحال می‌شود! چرا؟ چون یک مشکل را **قبل از خطر واقعی** پیدا کرده و می‌تواند تعمیرش کند.  
در برنامه‌نویسی هم دقیقاً همین کار را می‌کنیم و به آن می‌گوییم **تست‌نویسی (Testing)** – یکی از مهم‌ترین مهارت‌های یک **جادوگر کامپیوتر** برای اطمینان از درست کار کردن برنامه قبل از تحویل به دیگران. 🧙‍♂️

#### ۱۱.۱.۲. تست چیست؟
تست، یک تکه کد کوچک است که یک بخش از برنامه‌ی اصلی را صدا می‌زند و نتیجه‌اش را با چیزی که انتظار داشتیم مقایسه می‌کند.  
✅ اگر نتیجه همانی باشد که می‌خواستیم → تست سبز (پاس) می‌شود و چراغ اعتماد روشن می‌شود.  
❌ اگر نتیجه فرق کند → تست قرمز (فیل) می‌شود و کامپایلر دقیقاً می‌گوید کجا اشتباه کردیم.

#### ۱۱.۱.۳. اولین تست با `#[test]`
در Rust، برای تبدیل کردن یک تابع معمولی به یک تست، فقط کافی است یک برچسب جادویی بالای سرش بنویسیم: `#[test]`.  
داخل تابع هم از ابزارهای بررسی درستی (مثل `assert_eq!`) استفاده می‌کنیم:
```rust
#[test]
fn check_addition() {
    assert_eq!(2 + 2, 4);
}
```
این کد به کامپایلر می‌گوید: «این یک تست است. لطفاً چک کن که ۲+۲ واقعاً ۴ بشود!»

#### ۱۱.۱.۴. اجرای تست با `cargo test`
برای اجرای همه‌ی تست‌ها، در ترمینال و داخل پوشه‌ی پروژه بنویس:
```bash
cargo test
```
کارگو تمام فایل‌ها می‌گردد، توابعی که `#[test]` دارند را پیدا می‌کند و یکی‌یکی اجرایشان می‌کند.

#### ۱۱.۱.۵. خواندن خروجی تست
اگر همه‌چیز درست باشد، خروجی سبز و خوشگل است:
```
running 1 test
test check_addition ... ok

test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
```
اگر تستی شکست بخورد، با رنگ قرمز و اطلاعات کامل به تو نشان داده می‌شود:
```
failures:
---- check_addition stdout ----
thread 'check_addition' panicked at 'assertion failed: `(left == right)`
  left: `5`,
  right: `4`', src/lib.rs:3:5
```
کامپایلر دقیقاً می‌گوید: «من سمت چپ (`left`) را ۵ دیدم، ولی انتظار سمت راست (`right`) که ۴ بود را داشتم!»

![[Illustration: Cartoon cockpit labeled "SIMULATION MODE". Ferris the crab sits in the pilot seat, pressing buttons on a dashboard. Green checkmarks float above working systems, while a red warning light blinks on a "test failed" panel. Style: vibrant children's book illustration, playful tech metaphor, soft lighting, 16:9.]](../assets/images/11.1.png)

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> تست‌نویسی یکی از ارزشمندترین عادت‌های حرفه‌ای در برنامه‌نویسی است. این فصل نشان می‌دهد چطور با نوشتن تست، از درست کار کردن کد اطمینان حاصل کنیم. اگر کودک در ابتدا از نوشتن تست خسته شود، به او یادآوری کنید که تست مثل کمربند ایمنی است – شاید زحمت بستنش را داشته باشد، اما جانش را نجات می‌دهد. کتاب رسمی Rust فصل کاملی درباره‌ی تست دارد:  
> [doc.rust-lang.org/book/ch11-00-testing.html](https://doc.rust-lang.org/book/ch11-00-testing.html)

---

### ۱۱.۲. ماکروهای پرکاربرد تست

#### ۱۱.۲.۱. `assert!`
این ماکرو یک شرط می‌گیرد و چک می‌کند که حتماً `true` باشد. اگر `false` باشد، تست فیل می‌شود.
```rust
#[test]
fn test_is_positive() {
    let num = 5;
    assert!(num > 0); // درست است، پس رد می‌شود
}
```

#### ۱۱.۲.۲. `assert_eq!` و `assert_ne!`
🔹 `assert_eq!(چپ, راست)` : چک می‌کند دو مقدار دقیقاً مساوی باشند.  
🔹 `assert_ne!(چپ, راست)` : چک می‌کند دو مقدار **نامساوی** باشند.
```rust
fn add(a: i32, b: i32) -> i32 { a + b }

#[test]
fn test_add() {
    assert_eq!(add(2, 3), 5);   // باید ۵ باشد
    assert_ne!(add(2, 2), 10);  // نباید ۱۰ باشد
}
```

#### ۱۱.۲.۳. اضافه کردن پیام سفارشی
می‌توانی یک پیام دلخواه هم اضافه کنی تا اگر تست فیل شد، دقیق‌تر بفهمی چه اتفاقی افتاده:
```rust
#[test]
fn test_add_with_message() {
    let result = add(2, 2);
    assert_eq!(result, 5, "ما انتظار داشتیم ۵ شود، اما {} شد.", result);
}
```

#### ۱۱.۲.۴. `should_panic`
بعضی توابع طوری طراحی شده‌اند که در شرایط خاص باید بترکند (`panic!` کنند). مثلاً تابع تقسیم اگر مقسوم‌علیه صفر باشد. برای تست این حالت از `#[should_panic]` استفاده می‌کنیم:
```rust
fn divide(a: i32, b: i32) -> i32 {
    if b == 0 {
        panic!("تقسیم بر صفر ممنوع!");
    }
    a / b
}

#[test]
#[should_panic(expected = "تقسیم بر صفر")]
fn test_divide_by_zero() {
    divide(10, 0);
}
```
`expected` کمک می‌کند مطمئن شویم `panic` دقیقاً به خاطر همان دلیلی بوده که ما انتظار داشتیم.

#### ۱۱.۲.۵. تمرین: تست تابع `add`
یک تابع `add` بنویس که دو عدد را جمع کند. سپس سه تست برایش بنویس: جمع دو عدد مثبت، جمع مثبت و منفی، و جمع دو عدد منفی.
💡 **پاسخ نمونه:**
```rust
fn add(a: i32, b: i32) -> i32 { a + b }

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add_positive() { assert_eq!(add(2, 3), 5); }
    #[test]
    fn test_add_mixed() { assert_eq!(add(5, -3), 2); }
    #[test]
    fn test_add_negative() { assert_eq!(add(-2, -3), -5); }
}
```

![[Illustration: A friendly robot quality inspector holding a rubber stamp. One stamp says "assert_eq! ✅", the other "assert_ne! ❌". Ferris stands beside a conveyor belt of code blocks waiting for inspection. Style: clean educational cartoon, bright colors, clear visual metaphor, 16:9.]](../assets/images/11.2.png)

---

### ۱۱.۳. سازماندهی تست‌ها

#### ۱۱.۳.۱. تست‌های واحد (Unit Tests)
تست‌های واحد، کوچک‌ترین بخش‌های برنامه (مثل یک تابع یا متد) را به تنهایی آزمایش می‌کنند. این تست‌ها معمولاً **همان در فایلی که کد اصلی است** نوشته می‌شوند.

#### ۱۱.۳.۲. ماژول `tests` و `#[cfg(test)]`
برای جدا کردن کد تست از کد اصلی (و جلوگیری از کامپایل شدنش در نسخه‌ی نهایی)، تست‌ها را در یک ماژول به اسم `tests` می‌گذاریم و بالای آن `#[cfg(test)]` می‌نویسیم:
```rust
pub fn add(a: i32, b: i32) -> i32 { a + b }

#[cfg(test)]
mod tests {
    use super::*; // همه چیز از بیرون ماژول را بیاور اینجا

    #[test]
    fn test_add() { assert_eq!(add(2, 2), 4); }
}
```
`#[cfg(test)]` یعنی: «این ماژول را فقط وقتی کامپایل کن که دارم تست اجرا می‌کنم.» مثل یک اتاق مخفی که فقط موقع بازرسی باز می‌شود! 🕵️‍♂️

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> نوشتن تست ممکن است در ابتدا کمی خسته‌کننده به نظر برسد، اما هر چه بیشتر تمرین کنی، سریع‌تر و لذت‌بخش‌تر می‌شود. حتی برنامه‌نویسان حرفه‌ای هم وقتی باگ پیدا می‌کنند، اول از همه یک تست می‌نویسند تا مطمئن شوند دیگر آن باگ برنمی‌گردد.

#### ۱۱.۳.۳. تست‌های یکپارچه‌سازی (Integration Tests)
این تست‌ها برنامه را از دید یک **کاربر خارجی** آزمایش می‌کنند. این تست‌ها در یک پوشه‌ی جدا به اسم `tests/` (کنار پوشه‌ی `src/`) قرار می‌گیرند. هر فایل `.rs` در این پوشه مثل یک پروژه‌ی مستقل رفتار می‌کند و باید کتابخانه‌ی ما را `use` کند.
📂 ساختار:
```
my_project/
├── Cargo.toml
├── src/
│   └── lib.rs       // کد اصلی
└── tests/
    └── integration_test.rs // تست‌های بیرونی
```
مثال `tests/integration_test.rs`:
```rust
use my_project::add; // اسم پروژه‌ات را اینجا بنویس

#[test]
fn test_add_integration() {
    assert_eq!(add(2, 2), 4);
}
```

#### ۱۱.۳.۴. اجرای فقط یک تست
اگر پروژه بزرگ باشد، می‌توانی فقط یک تست خاص را اجرا کنی:
```bash
cargo test test_add_positive
```
حتی می‌توانی بخشی از اسم را بنویسی تا همه‌ی تست‌های مشابه اجرا شوند: `cargo test add`

#### ۱۱.۳.۵. نادیده گرفتن تست با `#[ignore]`
اگر تستی خیلی طولانی است یا هنوز آماده نیست، می‌توانی موقتاً غیرفعالش کنی:
```rust
#[test]
#[ignore]
fn long_running_test() { /* کدی که ۱۰ دقیقه طول می‌کشد */ }
```
برای اجرای تست‌های نادیده‌گرفته‌شده: `cargo test -- --ignored`

![[Illustration: Architectural blueprint of a codebase. Left side: main factory labeled "src". Right side: a hidden laboratory labeled "#[cfg(test)] mod tests" connected by a secret tunnel. Top side: an external inspection booth labeled "tests/ integration". Ferris points to the different zones. Style: playful technical diagram, children's book style, bright, 16:9.]](../assets/images/11.3.png)

---

### ۱۱.۴. پروژه: تست برای بازی حدس عدد (فصل ۲)

حالا وقتش است بازی حدس عدد را طوری بازنویسی کنیم که قابل تست باشد. (یادت هست؟ یک عدد تصادفی تولید می‌کرد، ورودی می‌گرفت و راهنمایی می‌کرد.)

#### ۱۱.۴.۱. تبدیل بازی به کتابخانه
اول یک پروژه‌ی کتابخانه‌ای می‌سازیم تا بتوانیم توابعش را تست بگیریم:
```bash
cargo new guess_game_lib --lib
cd guess_game_lib
```
در `Cargo.toml` وابستگی `rand` را اضافه کن (نسخه‌ی جدید):
```toml
[dependencies]
rand = "0.9.0"
```

#### ۱۱.۴.۲. تابع `generate_secret` با دانه ثابت
در تست‌ها نمی‌خواهیم عدد واقعاً تصادفی باشد (چون هر بار عوض می‌شود و نمی‌توانیم نتیجه را پیش‌بینی کنیم). پس یک تابع کمکی مخصوص تست می‌سازیم که همیشه یک عدد ثابت برگرداند:
```rust
// src/lib.rs
use rand::Rng;

pub fn generate_secret() -> u32 {
    rand::thread_rng().gen_range(1..=100)
}

#[cfg(test)]
pub fn generate_secret_fixed() -> u32 { 42 } // همیشه ۴۲ برمی‌گرداند
```

#### ۱۱.۴.۳. تابع `check_guess`
این تابع منطق اصلی بازی را دارد:
```rust
#[derive(Debug, PartialEq)]
pub enum GuessResult { TooLow, TooHigh, Correct }

pub fn check_guess(guess: u32, secret: u32) -> GuessResult {
    if guess < secret { GuessResult::TooLow }
    else if guess > secret { GuessResult::TooHigh }
    else { GuessResult::Correct }
}
```

#### ۱۱.۴.۴. نوشتن تست‌ها
حالا در `lib.rs` زیر ماژول `tests` تست‌ها را می‌نویسیم:
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_check_guess_too_low() {
        assert_eq!(check_guess(10, 42), GuessResult::TooLow);
    }

    #[test]
    fn test_check_guess_correct() {
        assert_eq!(check_guess(42, 42), GuessResult::Correct);
    }

    #[test]
    fn test_generate_secret_fixed() {
        assert_eq!(generate_secret_fixed(), 42);
    }
}
```

#### ۱۱.۴.۵. تست تابع `read_input` با شبیه‌سازی
چطور تابعی که از صفحه‌کلید می‌خواند را تست کنیم؟ به جای `stdin` واقعی، تابع را جوری می‌نویسیم که از هر چیزی که قابلیت خواندن داشته باشد (Trait `BufRead`) ورودی بگیرد. در تست، از `Cursor` استفاده می‌کنیم که مثل یک نوار ضبط صوت مجازی عمل می‌کند و متن را کاراکتر به کاراکتر می‌خواند.
```rust
use std::io::{BufRead, Cursor};

pub fn read_number<R: BufRead>(reader: &mut R) -> Result<u32, String> {
    let mut input = String::new();
    reader.read_line(&mut input)
        .map_err(|e| format!("خطای خواندن: {}", e))?;
    input.trim().parse()
        .map_err(|_| "لطفاً یک عدد معتبر وارد کن".to_string())
}
```
و تست آن:
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_read_number_ok() {
        let input = b"42\n"; // نوار مجازی
        let mut cursor = Cursor::new(input);
        assert_eq!(read_number(&mut cursor), Ok(42));
    }

    #[test]
    fn test_read_number_invalid() {
        let input = b"hello\n";
        let mut cursor = Cursor::new(input);
        assert!(read_number(&mut cursor).is_err());
    }
}
```

![[Illustration: Cartoon scene showing a "Mock Input" machine. A tape labeled "Cursor: b'42\n'" feeds into a reader slot. The machine outputs a glowing green "Ok(42)" ticket. Ferris operates the controls with a satisfied smile. Style: dynamic, educational, bright colors, technical metaphor for children, 16:9.]](../assets/images/11.4.png)

---

### ۱۱.۵. جمع‌بندی و چالش

#### ۱۱.۵.۱. مرور مفاهیم
در این فصل یاد گرفتی:  
✅ تست‌نویسی مثل شبیه‌ساز پرواز است: قبل از استفاده‌ی واقعی، همه‌چیز را امتحان می‌کنیم.  
✅ `#[test]` تابع را به تست تبدیل می‌کند و `cargo test` اجرایشان می‌کند.  
✅ `assert!`، `assert_eq!` و `assert_ne!` برای بررسی درستی استفاده می‌شوند.  
✅ `#[should_panic]` برای تست توابعی که باید عمداً بترکند به کار می‌رود.  
✅ تست‌های واحد در ماژول `#[cfg(test)]` و تست‌های یکپارچه‌سازی در پوشه‌ی `tests/` قرار می‌گیرند.  
✅ برای تست ورودی، از `BufRead` و `Cursor` استفاده می‌کنیم تا نیاز به تایپ واقعی نباشد.  
✅ **تست‌نویسی تو را به یک مهندس نرم‌افزار واقعی تبدیل می‌کند – کسی که قبل از اینکه کاربر دچار مشکل شود، مشکل را پیدا می‌کند.** 🧙

#### ۱۱.۵.۲. چالش: تست برای `struct Monster`
به `struct Monster` از فصل ۵ برگرد. یک متد `attack` به آن اضافه کن که به هیولای دیگر حمله کند و قدرتش را کم کند. سپس سه تست بنویس:
۱. حمله‌ای که قدرت قربانی را کاهش دهد.  
۲. حمله با قدرت صفر (نباید قدرتی کم شود).  
۳. چک کردن مقدار آسیب برگشتی.

💡 **پاسخ نمونه:**
```rust
struct Monster { name: String, power: u32 }

impl Monster {
    fn attack(&self, other: &mut Monster) -> u32 {
        let damage = self.power;
        other.power = other.power.saturating_sub(damage);
        damage
    }
}

#[cfg(test)]
mod monster_tests {
    use super::*;

    #[test]
    fn test_attack_reduces_power() {
        let mut victim = Monster { name: String::from("ضعیف"), power: 100 };
        let attacker = Monster { name: String::from("قوی"), power: 30 };
        attacker.attack(&mut victim);
        assert_eq!(victim.power, 70);
    }

    #[test]
    fn test_attack_with_zero_power() {
        let mut victim = Monster { name: String::from("قوی"), power: 100 };
        let attacker = Monster { name: String::from("بی‌آزار"), power: 0 };
        attacker.attack(&mut victim);
        assert_eq!(victim.power, 100); // باید همان ۱۰۰ بماند
    }

    #[test]
    fn test_attack_returns_damage() {
        let mut victim = Monster { name: String::from("قربانی"), power: 50 };
        let attacker = Monster { name: String::from("مهاجم"), power: 20 };
        let damage = attacker.attack(&mut victim);
        assert_eq!(damage, 20);
    }
}
```

حالا تو می‌دانی چطور با نوشتن تست، از درستی برنامه‌ات مطمئن شوی و با خیال راحت تغییرات جدید اضافه کنی. 🛡️✨  
در فصل بعد، یک پروژه‌ی کامل و حرفه‌ای خط فرمان (شبیه دستور `grep`) می‌سازیم و تمام چیزهایی که تا حالا یاد گرفتی را کنار هم می‌چینیم! 🔍📜

![[Illustration: Ferris wearing a graduation cap and safety goggles, holding a glowing "Chapter 11 Master" badge. Floating around him are testing tools: a green checkmark stamp, a red panic button, a mock tape reader, and a hidden lab door. Style: encouraging, vibrant children's book illustration, celebratory mood, 16:9.]](../assets/images/11.5.png)
