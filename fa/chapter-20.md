# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۲۰: فریس‌نت: شبکه‌ی مخفی دوستان (پروژه‌ی شبکه‌ی نهایی)

### 📑 فهرست فصل
[۲۰.۱. چطور فریس با دوستش در کامپیوتر دیگر حرف بزند؟ (Socket)](#۲۰۱-چطور-فریس-با-دوستش-در-کامپیوتر-دیگر-حرف-بزند-socket)  
[۲۰.۱.۱. داستان: تلفن‌های فضایی](#۲۰۱۱-داستان-تلفن‌های-فضایی)  
[۲۰.۱.۲. مفاهیم پایه: IP، پورت، کلاینت و سرور](#۲۰۱۲-مفاهیم-پایه-ip-پورت-کلاینت-و-سرور)  
[۲۰.۱.۳. جعبه ابزار شبکه: std::net](#۲۰۱۳-جعبه-ابزار-شبکه-stdnet)  
[۲۰.۲. ساختن یک پیام‌رسان ساده (Ferris Messenger)](#۲۰۲-ساختن-یک-پیام‌رسان-ساده-ferris-messenger)  
[۲۰.۲.۱. سرور: گوش دادن به درگاه](#۲۰۲۱-سرور-گوش-دادن-به-درگاه)  
[۲۰.۲.۲. کلاینت: اتصال و ارسال پیام](#۲۰۲۲-کلاینت-اتصال-و-ارسال-پیام)  
[۲۰.۲.۳. تمرین: ارسال پاسخ از سرور](#۲۰۲۳-تمرین-ارسال-پاسخ-از-سرور)  
[۲۰.۳. بهبود پیام‌رسان: چت دوطرفه](#۲۰۳-بهبود-پیام‌رسان-چت-دوطرفه)  
[۲۰.۳.۱. مشکل: نوبتی حرف زدن خسته‌کننده است](#۲۰۳۱-مشکل-نوبتی-حرف-زدن-خسته‌کننده-است)  
[۲۰.۳.۲. استفاده از دو ریسه برای خواندن و نوشتن](#۲۰۳۲-استفاده-از-دو-ریسه-برای-خواندن-و-نوشتن)  
[۲۰.۴. پروژه‌ی نهایی: چت گروهی فریس‌نت](#۲۰۴-پروژهی-نهایی-چت-گروهی-فریسنت)  
[۲۰.۴.۱. ایده: پخش پیام به همه](#۲۰۴۱-ایده-پخش-پیام-به-همه)  
[۲۰.۴.۲. لیست مهمان‌های اشتراکی](#۲۰۴۲-لیست-مهمان‌های-اشتراکی)  
[۲۰.۴.۳. کد کامل سرور چت گروهی](#۲۰۴۳-کد-کامل-سرور-چت-گروهی)  
[۲۰.۴.۴. کلاینت چت گروهی](#۲۰۴۴-کلاینت-چت-گروهی)  
[۲۰.۴.۵. چالش: اضافه کردن نام کاربری](#۲۰۴۵-چالش-اضافه-کردن-نام-کاربری)  
[۲۰.۵. خداحافظی و مسیر آینده](#۲۰۵-خداحافظی-و-مسیر-آینده)  
[۲۰.۵.۱. تبریک! تو یک Rustacean واقعی شدی](#۲۰۵۱-تبریک-تو-یک-rustacean-واقعی-شدی)  
[۲۰.۵.۲. قدم‌های بعدی](#۲۰۵۲-قدم‌های-بعدی)  
[۲۰.۵.۳. حرف آخر فریس](#۲۰۵۳-حرف-آخر-فریس)  

---

### ۲۰.۱. چطور فریس با دوستش در کامپیوتر دیگر حرف بزند؟ (Socket)

#### ۲۰.۱.۱. داستان: تلفن‌های فضایی
فریس دلش برای دوستش بیل تنگ شده که در سفینه‌ی کناری زندگی می‌کند. اما دیوارهای فلزی سفینه خیلی ضخیم‌اند و صدا از آن‌ها رد نمی‌شود. فریس یک فکر عالی می‌کند: «چرا از کامپیوترها برای حرف زدن استفاده نکنیم؟»  
کامپیوترها می‌توانند از طریق سیم‌ها یا امواج بی‌سیم، داده‌ها را برای هم بفرستند. اما چطور بفهمند پیام مال کدام برنامه است؟ مرورگر وب؟ بازی؟ یا برنامه‌ی چت؟ اینجاست که آدرس‌ها و پورت‌ها وارد می‌شوند! 📡✨  
**این آخرین گام تو برای تبدیل شدن به یک جادوگر کامپیوتر است – ساختن ارتباط بین دو کامپیوتر!** 🧙‍♂️

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> این پروژه ترکیبی از مفاهیم شبکه، هم‌روندی و مدیریت خطا است و یک دستاورد بزرگ برای پایان کتاب محسوب می‌شود. اگر کودک در اجرای پروژه‌ی چت گروهی مشکل داشت، می‌توانید ابتدا نسخه‌ی ساده (یک کلاینت) را اجرا کنید و بعد به سراغ نسخه‌ی چند کلاینت بروید. کتاب رسمی Rust فصل مفیدی درباره‌ی شبکه ندارد، اما مستندات `std::net` منبع خوبی است:  
> [doc.rust-lang.org/std/net/index.html](https://doc.rust-lang.org/std/net/index.html)

#### ۲۰.۱.۲. مفاهیم پایه: IP، پورت، کلاینت و سرور
برای درک شبکه، کافی است سه تا چیز را بدانی:
🔹 **آدرس IP:** مثل آدرس خانه است. هر کامپیوتر در شبکه یک شماره‌ی منحصر‌به‌فرد دارد. `127.0.0.1` یک آدرس ویژه است که همیشه به «همان کامپیوتر خودت» اشاره می‌کند (به آن می‌گویند `localhost`).
🔹 **پورت (Port):** مثل شماره‌ی واحد آپارتمان است. یک کامپیوتر می‌تواند همزمان چندین برنامه‌ی شبکه‌ای اجرا کند. هر برنامه روی یک پورت مشخص گوش می‌دهد. ما از پورت `7878` استفاده می‌کنیم.
🔹 **سرور و کلاینت:** سرور (Server) مثل پذیرش هتل می‌ماند که منتظر می‌ماند کسی بیاید. کلاینت (Client) مثل مهمانی است که در می‌زند و وصل می‌شود.

![[Illustration: Cartoon illustration of two friendly space crabs in separate spaceship cabins, talking via glowing walkie-talkies. Between them, a floating holographic map shows an IP address "127.0.0.1" and a port number "7878" connected by a dotted light beam. Style: vibrant children's book, playful tech metaphor, soft lighting, 16:9.]](../assets/images/20.1.png)

#### ۲۰.۱.۳. جعبه ابزار شبکه: `std::net`
خبر خوب این است که Rust یک ماژول آماده و عالی به اسم `std::net` دارد که همه‌ی ابزارهای لازم برای شبکه را داخل خودش دارد. ما در این فصل از پروتکل **TCP** استفاده می‌کنیم. TCP مثل یک تماس تلفنی مطمئن است: اول اتصال برقرار می‌شود، بعد پیام‌ها به ترتیب و بدون گم شدن رد و بدل می‌شوند. 📞

---

### ۲۰.۲. ساختن یک پیام‌رسان ساده (Ferris Messenger)

#### ۲۰.۲.۱. سرور: گوش دادن به درگاه
اول یک پروژه جدید می‌سازیم. سرور ما مثل یک نگهبان می‌ماند که دم در ایستاده و منتظر می‌ماند کسی بیاید:
```rust
use std::io::{Read, Write};
use std::net::TcpListener;

fn main() -> std::io::Result<()> {
    // ۱. یک شنونده روی آدرس خودمان و پورت ۷۸۷۸ می‌سازیم
    let listener = TcpListener::bind("127.0.0.1:7878")?;
    println!("🦀 سرور فریس روی پورت ۷۸۷۸ گوش می‌دهد...");

    // ۲. منتظر می‌مانیم تا کسی وصل شود
    for stream in listener.incoming() {
        let mut stream = stream?;
        println!("✅ یک کلاینت وصل شد!");

        // ۳. یک فضای خالی برای خواندن پیام درست می‌کنیم (۱۰۲۴ بایت)
        let mut buffer = [0; 1024];
        let n = stream.read(&mut buffer)?;

        // ۴. بایت‌ها را به متن تبدیل می‌کنیم
        let message = String::from_utf8_lossy(&buffer[..n]);
        println!("📩 پیام دریافت شد: {}", message);

        // ۵. یک پاسخ برمی‌گردانیم
        let response = "پیامت رسید! 👋";
        stream.write_all(response.as_bytes())?;
    }
    Ok(())
}
```
🔹 `TcpListener::bind` یک درگاه گوش‌به‌زنگ می‌سازد.  
🔹 `listener.incoming()` یک صف از اتصال‌های ورودی برمی‌گرداند.  
🔹 `stream.read` داده‌ها را می‌خواند و `write_all` پاسخ را می‌فرستد.

#### ۲۰.۲.۲. کلاینت: اتصال و ارسال پیام
حالا یک فایل دیگر به اسم `client.rs` می‌سازیم که مثل مهمان در می‌زند:
```rust
use std::io::{Read, Write};
use std::net::TcpStream;

fn main() -> std::io::Result<()> {
    // ۱. به سرور وصل می‌شویم
    let mut stream = TcpStream::connect("127.0.0.1:7878")?;
    println!("🔗 به سرور وصل شدیم!");

    // ۲. پیام را می‌فرستیم
    let msg = "سلام فریس! این پیام از طرف بیل است.";
    stream.write_all(msg.as_bytes())?;
    println!("📤 پیام ارسال شد: {}", msg);

    // ۳. منتظر پاسخ می‌مانیم
    let mut buffer = [0; 1024];
    let n = stream.read(&mut buffer)?;
    let response = String::from_utf8_lossy(&buffer[..n]);
    println!("📩 پاسخ سرور: {}", response);

    Ok(())
}
```
اگر سرور را در یک ترمینال و کلاینت را در ترمینال دیگر اجرا کنی، می‌بینی که پیام‌ها با موفقیت رد و بدل می‌شوند! 🎉

#### ۲۰.۲.۳. تمرین: ارسال پاسخ از سرور
سرور را تغییر بده تا به جای متن ثابت، همان پیام کلاینت را با حروف بزرگ (`to_uppercase()`) برگرداند.
💡 **راهنمایی:** کافی است خط `response` را به `let response = message.to_uppercase();` تغییر دهی.

![[Illustration: Split-screen educational graphic. Left: a cartoon server rack with a glowing "Listening..." sign. Right: a friendly laptop with a "Connecting..." progress bar. A glowing message bubble travels between them. Ferris watches with a checklist, smiling. Style: clean vector illustration, bright, educational metaphor, 16:9.]](../assets/images/20.2.png)

---

### ۲۰.۳. بهبود پیام‌رسان: چت دوطرفه

#### ۲۰.۳.۱. مشکل: نوبتی حرف زدن خسته‌کننده است
تا اینجا ارتباط ما مثل یک پیامک یک‌طرفه بود. اما چت واقعی باید دوطرفه باشد! هر دو طرف باید همزمان بتوانند تایپ کنند و پیام‌های طرف مقابل را ببینند.

#### ۲۰.۳.۲. استفاده از دو ریسه برای خواندن و نوشتن
برای حل این مشکل از دو تا **ریسه (Thread)** استفاده می‌کنیم (یادت می‌آید فصل ۱۶ چه گفتیم؟):
🔸 **ریسه‌ی ۱:** دائماً از صفحه‌کلید کاربر می‌خواند و به سرور می‌فرستد.  
🔸 **ریسه‌ی ۲:** دائماً از سرور می‌خواند و پیام‌ها را روی صفحه چاپ می‌کند.

این‌طوری هیچ‌کس منتظر نوبت نمی‌ماند! ⚡

```rust
use std::io::{self, BufRead, BufReader, Write};
use std::net::TcpStream;
use std::thread;

fn main() -> std::io::Result<()> {
    let mut stream = TcpStream::connect("127.0.0.1:7878")?;
    println!("🔗 به چت‌روم فریس وصل شدی! (برای خروج quit بنویس)");

    // یک کپی از سوکت برای ریسه‌ی دریافت پیام
    let mut stream_clone = stream.try_clone()?;

    // ریسه‌ی دریافت‌کننده: گوش می‌دهد به سرور
    let receiver = thread::spawn(move || {
        let reader = BufReader::new(&mut stream_clone);
        for line in reader.lines() {
            match line {
                Ok(msg) => println!("📩 {}", msg),
                Err(_) => {
                    println!("❌ اتصال با سرور قطع شد.");
                    break;
                }
            }
        }
    });

    // ریسه‌ی اصلی (فرستنده): گوش می‌دهد به صفحه‌کلید
    let stdin = io::stdin();
    for line in stdin.lock().lines() {
        let line = line?;
        if line.trim() == "quit" { break; }
        stream.write_all(line.as_bytes())?;
        stream.write_all(b"\n")?;
    }

    receiver.join().unwrap();
    println!("👋 خداحافظ!");
    Ok(())
}
```
📌 `stream.try_clone()` خیلی مهم است! سوکت‌ها مثل کلید هستند. نمی‌شود همزمان دو تا ریسه از یک سوکت استفاده کنند مگر اینکه یک کپی از آن ساخته شود.

![[Illustration: Cartoon scene showing a split pathway. Left side: a user typing on a keyboard, messages flowing UP to a server. Right side: messages flowing DOWN from the server to a screen. Two glowing threads labeled "Thread 1" and "Thread 2" weave together smoothly. Ferris stands in the middle conducting traffic like an orchestra leader. Style: dynamic, educational children's book, bright colors, 16:9.]](../assets/images/20.3.png)

---

### ۲۰.۴. پروژه‌ی نهایی: چت گروهی فریس‌نت

#### ۲۰.۴.۱. ایده: پخش پیام به همه
حالا می‌خواهیم یک چت‌روم واقعی بسازیم که هر کسی وارد شد، پیام‌هایش را به **همه‌ی** افراد دیگر بفرستد. درست مثل یک اتاق کلاس که هر کسی حرف بزند، همه می‌شنوند! 🗣️🌍

#### ۲۰.۴.۲. لیست مهمان‌های اشتراکی
سرور باید یک لیست از همه‌ی کسانی که وصل شده‌اند نگه دارد. وقتی یک پیام می‌آید، سرور آن را کپی می‌کند و برای همه‌ی لیست می‌فرستد.  
چون چندین ریسه همزمان به این لیست دسترسی دارند، باید از `Arc` (برای اشتراک‌گذاری) و `Mutex` (برای جلوگیری از تداخل نوشتن) استفاده کنیم:
```rust
type Clients = Arc<Mutex<Vec<TcpStream>>>;
```
این یعنی: «یک لیست امن و اشتراکی از سوکت‌ها».

#### ۲۰.۴.۳. کد کامل سرور چت گروهی
```rust
use std::io::{BufRead, BufReader, Write};
use std::net::{TcpListener, TcpStream};
use std::sync::{Arc, Mutex};
use std::thread;

type Clients = Arc<Mutex<Vec<TcpStream>>>;

fn main() -> std::io::Result<()> {
    let listener = TcpListener::bind("127.0.0.1:7878")?;
    println!("🦀 سرور چت گروهی روی پورت ۷۸۷۸ فعال است!");

    let clients: Clients = Arc::new(Mutex::new(Vec::new()));

    for stream in listener.incoming() {
        let mut stream = stream?;
        println!("✅ کاربر جدید وصل شد!");

        // اضافه کردن کلاینت به لیست
        clients.lock().unwrap().push(stream.try_clone()?);
        let clients_clone = Arc::clone(&clients);

        // یک ریسه‌ی جدید برای هر کاربر
        thread::spawn(move || {
            handle_client(stream, clients_clone);
        });
    }
    Ok(())
}

fn handle_client(mut stream: TcpStream, clients: Clients) {
    let reader = BufReader::new(&mut stream);
    
    for line in reader.lines() {
        match line {
            Ok(msg) => {
                let formatted = format!("[کاربر]: {}\n", msg);
                println!("📨 {}", formatted.trim());
                
                // پخش پیام به همه
                let mut clients_guard = clients.lock().unwrap();
                for client in clients_guard.iter_mut() {
                    // اگر نوشتن موفق نبود، نادیده می‌گیریم تا برنامه کرش نکند
                    let _ = client.write_all(formatted.as_bytes());
                }
            }
            Err(_) => break, // کاربر قطع شده
        }
    }
    println!("❌ یک کاربر خارج شد.");
}
```
💡 **نکته‌ی حرفه‌ای:** `let _ = client.write_all(...)` یعنی اگر نوشتن موفق نبود (مثلاً آن کلاینت رفته)، خطا را نادیده بگیر و برنامه را ادامه بده. این برای سرورهای واقعی خیلی مهم است!

#### ۲۰.۴.۴. کلاینت چت گروهی
کلاینت همان کد دوطرفه‌ی بخش قبلی است. برای اجرا، دو فایل جداگانه در یک پروژه یا دو پروژه‌ی جداگانه بسازید. می‌توانید در `Cargo.toml` دو باینری تعریف کنید:
```toml
[[bin]]
name = "server"
path = "src/server.rs"

[[bin]]
name = "client"
path = "src/client.rs"
```
سپس با `cargo run --bin server` و `cargo run --bin client` اجرا کنید. چند ترمینال باز کن، سرور را اجرا کن، و چند بار `cargo run --bin client` بزن. حالا هر چیزی در یک ترمینال تایپ کنی، در بقیه هم ظاهر می‌شود! 🎊

#### ۲۰.۴.۵. چالش: اضافه کردن نام کاربری
الان همه پیام‌ها با `[کاربر]` شروع می‌شوند. می‌توانی برنامه را طوری تغییر دهی که اول اسم کاربر را بپرسد و سرور همان را در پیام نشان بدهد؟  
💡 **راهنمایی:** اولین پیامی که کلاینت می‌فرستد می‌تواند اسمش باشد. سرور می‌تواند آن را بخواند و برای پیام‌های بعدی استفاده کند. یا ساده‌تر: کلاینت خودش قبل از هر پیام، `[اسم]: ` را اضافه کند.

![[Illustration: A cozy cartoon chat room with floating speech bubbles connecting three different laptops. Each screen shows a friendly avatar and messages flowing in real-time. In the center, a glowing server hub labeled "Arc<Mutex<Vec>>" safely routes messages. Ferris sits at a control desk giving a thumbs up. Style: warm, inviting children's book illustration, clear network metaphor, 16:9.]](../assets/images/20.4.png)

---

### ۲۰.۵. خداحافظی و مسیر آینده

#### ۲۰.۵.۱. تبریک! تو یک Rustacean واقعی شدی
بیست فصل پیش، تو نمی‌دانستی `fn main()` یعنی چه. امروز، تو یک شبکه‌ی اجتماعی ساده ساختی، هم‌روندی را فهمیدی، با اشاره‌گرهای هوشمند کار کردی، و مفاهیم پیشرفته‌ای مثل Traits و Generics را به کار گرفتی. تو حالا رسماً یک **Rustacean** هستی! 🦀🎉  
**تو از یک مبتدی که «سلام دنیا» را نوشت، به جادوگری رسیدی که می‌تواند بین کامپیوترها ارتباط برقرار کند. این یعنی قدرت واقعی!** 🧙✨

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> اگر در اجرای پروژه‌ی چت گروهی با مشکل مواجه شدی (مثل اینکه پیام‌ها به همه نرسید)، نگران نباش. اشکال‌زدایی برنامه‌های شبکه‌ای کمی حساس است. قدم به قدم پیش برو: اول مطمئن شو سرور و کلاینت تنها روی `127.0.0.1` کار می‌کنند، بعد به سراغ چند کلاینت برو. هر مشکلی را که حل کنی، یک گام بزرگ به جلو برداشته‌ای.

#### ۲۰.۵.۲. قدم‌های بعدی
یادگیری Rust اینجا تمام نمی‌شود. این تازه شروع ماجراست! این کارها را بعد از کتاب امتحان کن:
📖 **کتاب رسمی Rust:** "The Rust Programming Language" را آنلاین بخوان (رایگان است!).  
🧩 **تمرین‌های روزانه:** سایت‌های `rustlings` و `exercism` پر از چالش‌های کوچک و جذاب هستند.  
🌐 **جامعه‌ی Rust:** به انجمن‌ها یا Discord رسمی Rust بپیوند. پر از آدم‌های مهربانی است که عاشق راهنمایی کردن هستند.  
🛠️ **پروژه شخصی:** بهترین راه یادگیری، ساختن چیز جدید است! یک بازی ساده، یک ابزار خط فرمان، یا یک سایت کوچک با فریم‌ورک‌هایی مثل `Axum` بساز.  
⚡ **برنامه‌نویسی Async:** با `async/await` و کتابخانه‌ی `tokio` آشنا شو تا برنامه‌های شبکه‌ای فوق‌سریع بنویسی.

#### ۲۰.۵.۳. حرف آخر فریس
> *«دوست من، تو فوق‌العاده‌ای! تو از پس سخت‌ترین مفاهیم برآمدی و نشان دادی که با کمی صبر و تمرین، هر چیزی ممکن است. من (فریس) به تو افتخار می‌کنم. حالا سفینه‌ی تو آماده‌ی پرواز به کهکشان‌های دور برنامه‌نویسی است. 🚀*  
> *یادت باشد: کامپایلر دوست تو است، نه دشمنت. اشتباه کردن یعنی داری یاد می‌گیری. ساده‌ترین کدی که کار کند، از پیچیده‌ترین کدی که کار نکند بهتر است.*  
> *برو و کد بزن، بساز، خراب کن، و دوباره بساز. دنیای نرم‌افزار به امثال تو نیاز دارد. خداحافظ، Rustacean عزیز. تا ماجرای بعدی... 🦀💙»*

![[Illustration: Ferris the crab standing proudly on a small wooden crate labeled "Chapter 20 Complete". He holds a glowing Rust gear in one claw and waves with the other. Behind him, a starry galaxy forms the shape of a heart. Floating text: "Thank You for Coding!". Style: emotional, celebratory children's book illustration, warm sunset lighting, 16:9.]](../assets/images/20.5.png)
