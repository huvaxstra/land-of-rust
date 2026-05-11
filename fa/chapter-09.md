# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۹: وقتی سفینه خراب می‌شود! (مدیریت خطا)

### 📑 فهرست فصل
[۹.۱. دکمه‌ی قرمز را نزن! (panic!)](#۹۱-دکمه‌ی-قرمز-را-نزن-panic)  
[۹.۱.۱. داستان: دکمه خودتخریب سفینه](#۹۱۱-داستان-دکمه-خودتخریب-سفینه)  
[۹.۱.۲. panic! در عمل](#۹۱۲-panic-در-عمل)  
[۹.۱.۳. چه زمانی panic رخ می‌دهد؟](#۹۱۳-چه-زمانی-panic-رخ-می‌دهد)  
[۹.۱.۴. دیدن مسیر خطا با RUST_BACKTRACE](#۹۱۴-دیدن-مسیر-خطا-با-rust_backtrace)  
[۹.۱.۵. تمرین: panic عمدی](#۹۱۵-تمرین-panic-عمدی)  
[۹.۲. چراغ هشدار (Result)](#۹۲-چراغ-هشدار-result)  
[۹.۲.۱. داستان: چراغ‌های هشدار سفینه](#۹۲۱-داستان-چراغ‌های-هشدار-سفینه)  
[۹.۲.۲. معرفی Result<T, E>](#۹۲۲-معرفی-resultt-e)  
[۹.۲.۳. مثال: باز کردن فایل](#۹۲۳-مثال-باز-کردن-فایل)  
[۹.۲.۴. روش‌های برخورد با Result](#۹۲۴-روش‌های-برخورد-با-result)  
[۹.۲.۵. تمرین: تبدیل رشته به عدد با Result](#۹۲۵-تمرین-تبدیل-رشته-به-عدد-با-result)  
[۹.۳. روش فریس برای نجات (?) اپراتور](#۹۳-روش-فریس-برای-نجات-اپراتور)  
[۹.۳.۱. داستان: اپراتور جادویی نجات](#۹۳۱-داستان-اپراتور-جادویی-نجات)  
[۹.۳.۲. استفاده از ? در توابعی که Result برمی‌گردانند](#۹۳۲-استفاده-از--در-توابعی-که-result-برمی‌گردانند)  
[۹.۳.۳. زنجیره کردن ?](#۹۳۳-زنجیره-کردن-)  
[۹.۳.۴. ? با Option](#۹۳۴--با-option)  
[۹.۳.۵. تبدیل خطاها با map_err](#۹۳۵-تبدیل-خطاها-با-map_err)  
[۹.۳.۶. تمرین: خواندن دو عدد از فایل و تقسیم](#۹۳۶-تمرین-خواندن-دو-عدد-از-فایل-و-تقسیم)  
[۹.۴. پروژه: ماشین حساب مقاوم به خطا](#۹۴-پروژه-ماشین-حساب-مقاوم-به-خطا)  
[۹.۴.۱. دریافت عبارت از کاربر](#۹۴۱-دریافت-عبارت-از-کاربر)  
[۹.۴.۲. تابع parse_expression](#۹۴۲-تابع-parse_expression)  
[۹.۴.۳. تابع calculate](#۹۴۳-تابع-calculate)  
[۹.۴.۴. حلقه اصلی با مدیریت خطا](#۹۴۴-حلقه-اصلی-با-مدیریت-خطا)  
[۹.۵. جمع‌بندی و چالش](#۹۵-جمع‌بندی-و-چالش)  
[۹.۵.۱. مرور مفاهیم](#۹۵۱-مرور-مفاهیم)  
[۹.۵.۲. چالش: ماشین حساب با چهار عمل](#۹۵۲-چالش-ماشین-حساب-با-چهار-عمل)  

---

### ۹.۱. دکمه‌ی قرمز را نزن! (panic!)

#### ۹.۱.۱. داستان: دکمه خودتخریب سفینه
در اتاق فرمان سفینه‌ی فریس، یک دکمه‌ی قرمز بزرگ و براق وجود دارد که زیرش نوشته: `⛔ فشار ندهید! خودتخریب فوری`. فریس می‌داند اگر کسی این دکمه را بزند، سفینه در یک چشم به هم زدن نابود می‌شود و هیچ راه برگشتی نیست.  
در دنیای Rust هم دقیقاً همین دکمه را داریم: `panic!`. وقتی `panic!` اجرا شود، برنامه فوراً متوقف می‌شود، یک پیام خطا چاپ می‌کند و از کار می‌افتد. درست مثل انفجار سفینه! 💥

**یادگیری تشخیص خطاهای جبران‌ناپذیر از خطاهای قابل مدیریت، یکی از مهارت‌های اساسی یک جادوگر کامپیوتر است.** 🧙‍♂️

#### ۹.۱.۲. panic! در عمل
بیا خودمان یک `panic!` عمدی ایجاد کنیم:
```rust
fn main() {
    panic!("سفینه خراب شد! همه جا آتش گرفته است! 🔥");
}
```
اگر این کد را اجرا کنی، خروجی شبیه این می‌شود:
```
thread 'main' panicked at 'سفینه خراب شد! همه جا آتش گرفته است! 🔥', src/main.rs:2:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```
برنامه کلاً می‌ایستد و دستورات بعدش اصلاً اجرا نمی‌شوند.

#### ۹.۱.۳. چه زمانی panic رخ می‌دهد؟
علاوه بر اینکه خودمان `panic!` صدا بزنیم، بعضی کارهای خطرناک هم باعثش می‌شوند:
🔹 دسترسی به اندیس ناموجود در وکتور: `vec![1,2,3][99]`  
🔹 استفاده از `unwrap()` روی `None` یا `Err`  
🔹 تقسیم بر صفر در حالت debug  
مثال:
```rust
let v = vec![10, 20, 30];
println!("{}", v[10]); // panic: index out of bounds
```

#### ۹.۱.۴. دیدن مسیر خطا با RUST_BACKTRACE
وقتی `panic` می‌کند، Rust می‌تواند مسیر کامل اتفاقی که افتاده را نشان بدهد (مثل ردپای یک کارآگاه!). برای این کار، برنامه را با این متغیر محیطی اجرا کن:
```bash
RUST_BACKTRACE=1 cargo run
```
با این کار لیستی از توابعی که پشت سر هم صدا زده شده‌اند می‌بینی و می‌فهمی مشکل دقیقاً از کجا شروع شده است. 🔍

#### ۹.۱.۵. تمرین: panic عمدی
برنامه‌ای بنویس که یک وکتور ۵ عنصری از اعداد داشته باشد و از کاربر یک اندیس بخواهد. سپس آن عنصر را چاپ کند. اگر کاربر اندیسی خارج از محدوده وارد کرد، برنامه `panic` کند. (سعی کن با `RUST_BACKTRACE=1` اجرا کنی و خروجی را ببینی.)

![[Illustration: Close-up cartoon illustration of a shiny red emergency button labeled "panic!" on a spaceship control panel. A warning tape surrounds it. Ferris the crab stands nearby with a shocked expression, holding his claws up to stop someone from pressing it. Style: vibrant, dramatic but child-friendly, high contrast, 16:9.]](../assets/images/9.1.png)

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> این فصل دو نوع خطا را معرفی می‌کند: جبران‌ناپذیر (`panic!`) و قابل جبران (`Result`). درک این تفاوت یک مهارت مهندسی کلیدی است. کتاب رسمی Rust فصل کاملی درباره‌ی مدیریت خطا دارد:  
> [doc.rust-lang.org/book/ch09-00-error-handling.html](https://doc.rust-lang.org/book/ch09-00-error-handling.html)

---

### ۹.۲. چراغ هشدار (Result)

#### ۹.۲.۱. داستان: چراغ‌های هشدار سفینه
در سفینه‌ی فریس، یک سری چراغ هشدار زرد و نارنجی هم هست. مثلاً اگر موتور بیش از حد داغ شود، چراغ زرد روشن می‌شود و یک پیام می‌آید: `⚠️ موتور داغ کرده، ۳۰ ثانیه صبر کن`. این یک خطای قابل پیش‌بینی و قابل مدیریت است. فریس می‌تواند صبر کند تا موتور خنک شود و بعد حرکت کند.  
در Rust برای این نوع خطاها از `Result` استفاده می‌کنیم. این یعنی: «یا همه‌چیز خوب پیش رفته، یا یک مشکلی پیش آمده که می‌شود مدیریتش کرد.» 🟡

#### ۹.۲.۲. معرفی `Result<T, E>`
`Result` یک `enum` بسیار پرکاربرد در Rust است:
```rust
enum Result<T, E> {
    Ok(T),   // همه‌چیز خوب است و مقدار T برگردانده شده
    Err(E),  // یک خطا از نوع E رخ داده
}
```
🔹 `T`: نوع موفقیت (چیزی که اگر کار درست پیش برود برمی‌گردد).  
🔹 `E`: نوع خطا (چیزی که اگر مشکلی پیش بیاید برمی‌گردد).

#### ۹.۲.۳. مثال: باز کردن فایل
تابع `File::open` سعی می‌کند یک فایل را باز کند. ممکن است فایل وجود نداشته باشد یا دسترسی نداشته باشیم. پس یک `Result<File, std::io::Error>` برمی‌گرداند:
```rust
use std::fs::File;

fn main() {
    let file_result = File::open("hello.txt");
    // file_result می‌تواند Ok(File) باشد یا Err(Error)
}
```

#### ۹.۲.۴. روش‌های برخورد با Result
🔸 **روش سریع ولی خطرناک: `unwrap()` و `expect()`**  
اگر بگویی `unwrap()`، یعنی «اگر خطا بود، برنامه بترکد!». اگر `expect(msg)` بزنی، همان کار را می‌کند ولی با پیام دلخواه خودت.
```rust
let file = File::open("hello.txt").expect("نتوانستم فایل را باز کنم! 📁");
```
⚠️ **هشدار:** فقط در کدهای آزمایشی یا وقتی ۱۰۰٪ مطمئنی خطایی رخ نمی‌دهد از آنها استفاده کن!

🔸 **روش اصولی: `match`**  
می‌توانی هر دو حالت را بررسی کنی:
```rust
use std::fs::File;
use std::io::ErrorKind;

let file = match File::open("hello.txt") {
    Ok(f) => f,
    Err(error) => match error.kind() {
        ErrorKind::NotFound => {
            println!("فایل پیدا نشد. یک فایل جدید می‌سازم. 🛠️");
            File::create("hello.txt").expect("خطا در ساخت")
        }
        _ => panic!("یک خطای پیش‌بینی‌نشده رخ داد! 😱"),
    },
};
```

🔸 **روش تمیزتر: `unwrap_or_else`**  
یک تابع بی‌نام (closure) می‌گیرد و فقط اگر خطا رخ بده اجرایش می‌کند:
```rust
let file = File::open("hello.txt").unwrap_or_else(|error| {
    panic!("خطا رخ داد: {:?}", error);
});
```

#### ۹.۲.۵. تمرین: تبدیل رشته به عدد با Result
تابعی به اسم `parse_number` بنویس که یک `&str` بگیرد و سعی کند آن را به `i32` تبدیل کند. اگر موفق شد `Ok(num)` برگرداند، وگرنه `Err(String)` با پیام مناسب.

💡 **پاسخ نمونه:**
```rust
fn parse_number(s: &str) -> Result<i32, String> {
    s.trim()
        .parse()
        .map_err(|_| format!("'{}' یک عدد معتبر نیست 🔢", s))
}

fn main() {
    let inputs = ["42", "سلام", "-5", "3.14"];
    for inp in inputs {
        match parse_number(inp) {
            Ok(n) => println!("{} -> عدد: {}", inp, n),
            Err(e) => println!("{} -> خطا: {}", inp, e),
        }
    }
}
```

![[Illustration: Cartoon dashboard with two glowing indicators. Left: a green "OK" light shining on a wrapped gift labeled "T". Right: a yellow "Warning" light flashing over a toolbox labeled "E". Ferris stands between them holding a checklist, looking thoughtful. Style: educational metaphor, clean vector, bright colors, 16:9.]](../assets/images/9.2.png)

---

### ۹.۳. روش فریس برای نجات (?) اپراتور

#### ۹.۳.۱. داستان: اپراتور جادویی نجات
فریس یک ابزار جادویی به شکل علامت سؤال (`?`) دارد. هر وقت یک چراغ هشدار روشن می‌شود (یعنی یک `Result` از نوع `Err` برمی‌گردد)، او می‌تواند این علامت را بگذارد و بگوید: «اگر خطایی رخ داد، فوراً از این تابع خارج شو و خطا را به تابع بالاتر منتقل کن.» این کار را خیلی ساده می‌کند و دیگر نیازی به نوشتن `match` طولانی نیست! ✨

#### ۹.۳.۲. استفاده از `?` در توابعی که Result برمی‌گردانند
فرض کن می‌خواهیم تابعی بنویسیم که نام کاربری را از یک فایل بخواند. با `?` این‌طور می‌شود:
```rust
use std::fs::File;
use std::io::{self, Read};

fn read_username() -> Result<String, io::Error> {
    let mut file = File::open("username.txt")?;
    let mut username = String::new();
    file.read_to_string(&mut username)?;
    Ok(username)
}
```
اگر `File::open` خطا بدهد، `?` بلافاصله همان خطا را برمی‌گرداند و ادامه اجرا نمی‌شود. اگر `read_to_string` هم خطا بدهد، همان اتفاق می‌افتد. اگر همه‌چیز خوب پیش رفت، `Ok(username)` برگردانده می‌شود.

> 💡 **نکته:** اپراتور `?` فقط در توابعی می‌تواند استفاده شود که نوع خروجی آن `Result` (یا `Option`) باشد. اگر خروجی تابع `Result` نباشد، کامپایلر خطا می‌دهد.

#### ۹.۳.۳. زنجیره کردن `?`
می‌توانی چند `?` را پشت سر هم بگذاری تا کد کوتاه‌تر شود:
```rust
fn read_username_short() -> Result<String, io::Error> {
    let mut s = String::new();
    File::open("username.txt")?.read_to_string(&mut s)?;
    Ok(s)
}
```

#### ۹.۳.۴. `?` با Option
اپراتور `?` روی `Option` هم کار می‌کند. اگر `Option` برابر `None` باشد، تابع زودتر `None` برمی‌گرداند:
```rust
fn first_char(s: &str) -> Option<char> {
    s.chars().next()? // اگر s خالی باشد، None برمی‌گردد
}
```

#### ۹.۳.۵. تبدیل خطاها با `map_err`
گاهی نوع خطای تابع با نوع خطایی که باید برگردانیم فرق دارد. مثلاً می‌خواهیم همه خطاها را به `String` تبدیل کنیم تا راحت‌تر چاپ شوند. از `map_err` استفاده می‌کنیم:
```rust
use std::fs::File;
use std::io::Read;

fn read_number_from_file(filename: &str) -> Result<i32, String> {
    let mut s = String::new();
    File::open(filename)
        .map_err(|e| format!("باز کردن {}: {}", filename, e))?  // اگر خطا باشد، تبدیلش کن بعد برگردان
        .read_to_string(&mut s)
        .map_err(|e| format!("خواندن {}: {}", filename, e))?;
    s.trim().parse()
        .map_err(|_| format!("عدد معتبر در {} نیست", filename))
}
```
`map_err` یعنی «اگر خطا بود، قبل از برگرداندنش، با یک تابع دیگر تبدیلش کن». تابع داخل `map_err` (همان `|e| format!(...)`) یک **تابع بی‌نام** است که خطا را می‌گیرد و یک `String` برمی‌گرداند.

#### ۹.۳.۶. تمرین: خواندن دو عدد از فایل و تقسیم
دو فایل `a.txt` و `b.txt` فرضی داریم که هر کدام یک عدد دارند. تابعی بنویس که این دو عدد را بخواند و حاصل تقسیم `a / b` را به صورت `f64` برگرداند. اگر هر خطایی رخ داد (فایل نبود، عدد نبود، تقسیم بر صفر)، یک `String` مناسب برگردان.

💡 **پاسخ نمونه:**
```rust
use std::fs::File;
use std::io::Read;

fn read_number(filename: &str) -> Result<i32, String> {
    let mut s = String::new();
    File::open(filename)
        .map_err(|e| format!("{}: {}", filename, e))?
        .read_to_string(&mut s)
        .map_err(|e| format!("{}: {}", filename, e))?;
    s.trim().parse().map_err(|_| format!("{}: عدد معتبر نیست", filename))
}

fn divide_files() -> Result<f64, String> {
    let a = read_number("a.txt")?;
    let b = read_number("b.txt")?;
    if b == 0 {
        return Err(String::from("تقسیم بر صفر ممنوع! ⛔"));
    }
    Ok(a as f64 / b as f64)
}
```

![[Illustration: A magical floating question mark tool (?) glowing with a soft blue light, acting like a shortcut tunnel. On one side, a long winding path labeled "match match match". On the other side, a straight fast road through the "?" tunnel. Ferris happily zooms through the shortcut. Style: dynamic, educational cartoon, bright, 16:9.]](../assets/images/9.3.png)

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> تصمیم‌گیری بین `panic!` و `Result` – به خصوص زمانی که باید خطا را به بالا منتقل کنی – مهارتی است که حتی برنامه‌نویسان حرفه‌ای هم سال‌ها به آن مسلط می‌شوند. اگر هنوز در بعضی موارد احساس سردرگمی می‌کنی، نگران نباش. هر بار که از `Result` و `?` استفاده کنی، برایت طبیعی‌تر می‌شود.

---

### ۹.۴. پروژه: ماشین حساب مقاوم به خطا

حالا وقتش است یک برنامه‌ی واقعی بسازیم که هرگز کرش نکند! یک ماشین حساب ساده که چهار عمل اصلی را انجام بدهد و خطاها را مثل یک حرفه‌ای مدیریت کند. 🧮

#### ۹.۴.۱. دریافت عبارت از کاربر
کاربر عبارتی مثل `10 + 2` یا `8 / 0` وارد می‌کند. برنامه تا وقتی که کاربر `quit` ننوشته ادامه می‌دهد.

#### ۹.۴.۲. تابع `parse_expression`
این تابع رشته‌ی ورودی را تکه‌تکه می‌کند و سه بخش عدد اول، عملگر، عدد دوم را برمی‌گرداند. اگر فرمت اشتباه باشد خطا می‌دهد.
```rust
fn parse_expression(expr: &str) -> Result<(f64, char, f64), String> {
    let parts: Vec<&str> = expr.split_whitespace().collect();
    if parts.len() != 3 {
        return Err("فرمت باید 'عدد عملگر عدد' باشد (مثلاً 5 + 3) 📝".to_string());
    }
    let a = parts[0].parse::<f64>()
        .map_err(|_| format!("'{}' عدد اول معتبری نیست 🔢", parts[0]))?;
    let op = parts[1].chars().next()
        .ok_or("عملگر باید یک کاراکتر باشد (مثلاً +) 🔣".to_string())?;
    let b = parts[2].parse::<f64>()
        .map_err(|_| format!("'{}' عدد دوم معتبری نیست 🔢", parts[2]))?;
    Ok((a, op, b))
}
```

#### ۹.۴.۳. تابع `calculate`
```rust
fn calculate(a: f64, op: char, b: f64) -> Result<f64, String> {
    match op {
        '+' => Ok(a + b),
        '-' => Ok(a - b),
        '*' => Ok(a * b),
        '/' => {
            if b == 0.0 {
                Err("تقسیم بر صفر ممکن نیست! ⛔".to_string())
            } else {
                Ok(a / b)
            }
        }
        _ => Err(format!("عملگر '{}' پشتیبانی نمی‌شود. از + - * / استفاده کن. ⚠️", op)),
    }
}
```

#### ۹.۴.۴. حلقه اصلی با مدیریت خطا
```rust
use std::io::{self, Write};

fn main() {
    println!("🧮 ماشین حساب مقاوم فریس 🧮");
    println!("مثال: 10 + 5");
    println!("برای خروج 'quit' را بنویس.\n");

    loop {
        print!("> ");
        io::stdout().flush().unwrap();

        let mut input = String::new();
        io::stdin().read_line(&mut input).unwrap();
        let input = input.trim();

        if input == "quit" { break; }

        match parse_expression(input) {
            Ok((a, op, b)) => match calculate(a, op, b) {
                Ok(result) => println!("= {} ✅", result),
                Err(e) => println!("❌ خطا: {}", e),
            },
            Err(e) => println!("❌ خطا در ورودی: {}", e),
        }
    }
    println!("خدانگهدار! 🦀✨");
}
```

![[Illustration: A cozy cartoon desk with a retro-style calculator that has a glowing screen. Around it float colorful math symbols (+, -, *, /) and a small shield icon labeled "Error Safe". Ferris types on a keyboard with a confident smile. Style: warm, educational, children's book illustration, 16:9.]](../assets/images/9.4.png)

---

### ۹.۵. جمع‌بندی و چالش

#### ۹.۵.۱. مرور مفاهیم
در این فصل یاد گرفتی:  
✅ `panic!`: دکمه‌ی قرمز خودتخریب. برای خطاهای غیرقابل جبران.  
✅ `Result<T, E>`: برای خطاهای قابل پیش‌بینی و مدیریت.  
✅ `unwrap()` / `expect()`: روش سریع ولی خطرناک (اگر خطا باشد برنامه می‌ترکد).  
✅ `match`: روش اصولی برای بررسی تک‌تک حالات.  
✅ اپراتور `?`: ابزار جادویی برای خروج زودهنگام و انتشار خطا (فقط در توابعی که `Result` برمی‌گردانند).  
✅ `map_err`: تبدیل نوع خطا به زبان دلخواه ما.  
✅ **مدیریت هوشمندانه خطاها یعنی نوشتن برنامه‌هایی که هیچ‌وقت بی‌اجازه از کار نمی‌افتند – این نشانه‌ی یک جادوگر کامپیوتر حرفه‌ای است.** 🧙

#### ۹.۵.۲. چالش: ماشین حساب با چهار عمل
همان پروژه‌ی بالا را کامل کن و یک قابلیت جدید به آن اضافه کن: اگر کاربر ورودی را به صورت `10+5` (بدون فاصله) وارد کرد هم بتوانی پردازش کنی.  
💡 **راهنمایی:** می‌توانی از `split` روی کاراکترهای `+`، `-`، `*`، `/` استفاده کنی یا یک حلقه بزنی و اولین عملگر را پیدا کنی، بعد رشته را از همانجا جدا کنی.

حالا تو می‌دانی چطور خطاها را مثل یک قهرمان مدیریت کنی و برنامه‌هایی بنویسی که به جای ترکیدن، کاربر را راهنمایی می‌کنند. در فصل بعد، با **Generics و Traits** آشنا می‌شویم؛ ابزارهایی که به ما اجازه می‌دهند کدهای همه‌کاره و قابل استفاده‌ی مجدد بنویسیم، درست مثل یک آچار فرانسه‌ی فضایی! 🔧🌌

![[Illustration: Ferris wearing a superhero cape, holding a glowing "Chapter 9 Master" badge. Floating around him are safe shields, Result enums, panic buttons with red X marks, and a question mark tool. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/9.5.png)
