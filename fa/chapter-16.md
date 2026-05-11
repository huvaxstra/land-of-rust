# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۱۶: دسته‌های مورچه (هم‌روندی)

### 📑 فهرست فصل
[۱۶.۱. چطور یک لشکر مورچه یک برگ را جابجا می‌کنند؟ (Threads)](#۱۶۱-چطور-یک-لشکر-مورچه-یک-برگ-را-جابجا-می‌کنند-threads)  
[۱۶.۱.۱. داستان: مورچه‌ها و برگ بزرگ](#۱۶۱۱-داستان-مورچه‌ها-و-برگ-بزرگ)  
[۱۶.۱.۲. ریسه (Thread) چیست؟](#۱۶۱۲-ریسه-thread-چیست)  
[۱۶.۱.۳. ایجاد ریسه با thread::spawn](#۱۶۱۳-ایجاد-ریسه-با-threadspawn)  
[۱۶.۱.۴. منتظر ماندن با join](#۱۶۱۴-منتظر-ماندن-با-join)  
[۱۶.۱.۵. تمرین: دو ریسه همزمان](#۱۶۱۵-تمرین-دو-ریسه-همزمان)  
[۱۶.۲. انتقال داده بین ریسه‌ها](#۱۶۲-انتقال-داده-بین-ریسه‌ها)  
[۱۶.۲.۱. حرکت دادن مالکیت با move](#۱۶۲۱-حرکت-دادن-مالکیت-با-move)  
[۱۶.۲.۲. کانال (mpsc) برای ارسال پیام](#۱۶۲۲-کانال-mpsc-برای-ارسال-پیام)  
[۱۶.۲.۳. فرستادن چند پیام](#۱۶۲۳-فرستادن-چند-پیام)  
[۱۶.۲.۴. دریافت غیرمسدود با try_recv](#۱۶۲۴-دریافت-غیرمسدود-با-try_recv)  
[۱۶.۲.۵. تمرین: تولیدکننده و مصرف‌کننده](#۱۶۲۵-تمرین-تولیدکننده-و-مصرف‌کننده)  
[۱۶.۳. راهروی باریک (Mutex)](#۱۶۳-راهروی-باریک-mutex)  
[۱۶.۳.۱. داستان: راهروی یک نفره](#۱۶۳۱-داستان-راهروی-یک-نفره)  
[۱۶.۳.۲. Mutex<T> چیست؟](#۱۶۳۲-mutext-چیست)  
[۱۶.۳.۳. قفل کردن و دسترسی](#۱۶۳۳-قفل-کردن-و-دسترسی)  
[۱۶.۳.۴. به اشتراک گذاری بین ریسه‌ها با Arc](#۱۶۳۴-به-اشتراک-گذاری-بین-ریسه‌ها-با-arc)  
[۱۶.۳.۵. تمرین: شمارنده‌ی اشتراکی](#۱۶۳۵-تمرین-شمارنده‌ی-اشتراکی)  
[۱۶.۴. پروژه: شمارشگر همزمان با ریسه‌ها](#۱۶۴-پروژه-شمارشگر-همزمان-با-ریسه‌ها)  
[۱۶.۴.۱. بدون Mutex: مسابقه داده (Data Race)](#۱۶۴۱-بدون-mutex-مسابقه-داده-data-race)  
[۱۶.۴.۲. با Mutex: راه‌حل درست](#۱۶۴۲-با-mutex-راه‌حل-درست)  
[۱۶.۴.۳. اجرا و مشاهده نتیجه](#۱۶۴۳-اجرا-و-مشاهده-نتیجه)  
[۱۶.۵. جمع‌بندی و چالش](#۱۶۵-جمع‌بندی-و-چالش)  
[۱۶.۵.۱. مرور مفاهیم](#۱۶۵۱-مرور-مفاهیم)  
[۱۶.۵.۲. چالش: تولیدکننده-مصرف‌کننده با صف](#۱۶۵۲-چالش-تولیدکننده-مصرف‌کننده-با-صف)

---

### ۱۶.۱. چطور یک لشکر مورچه یک برگ را جابجا می‌کنند؟ (Threads)

#### ۱۶.۱.۱. داستان: مورچه‌ها و برگ بزرگ
تا حالا دقت کرده‌ای یک مورچه‌ی تنها نمی‌تواند یک برگ بزرگ را تکان دهد؟ 🍃 ولی وقتی هزاران مورچه با هم همکاری می‌کنند، آن برگ مثل یک قایق سبک روی دوششان حرکت می‌کند. هر مورچه یک گوشه را گرفته و همزمان با بقیه زور می‌زند.  
در دنیای کامپیوتر، به این مورچه‌های کوشا می‌گوییم **ریسه (Thread)**. با استفاده از ریسه‌ها می‌توانیم چند تا کار را همزمان انجام دهیم و برنامه‌هایمان را سریع‌تر و قدرتمندتر کنیم.  
**یادگیری هم‌روندی یعنی می‌توانی از قدرت واقعی کامپیوترهای چند هسته‌ای استفاده کنی – گامی بزرگ به سوی جادوگر کامپیوتر شدن!** 🧙‍♂️

#### ۱۶.۱.۲. ریسه (Thread) چیست؟
یک ریسه مثل یک کارگر کوچک داخل برنامه‌ی تو است. برنامه‌ی اصلی تو (تابع `main`) خودش یک ریسه است (به آن می‌گوییم ریسه‌ی اصلی). تو می‌توانی به ریسه‌ی اصلی بگویی: «برو چند تا کارگر جدید استخدام کن و کارها را بینشان تقسیم کن!» همه‌ی این کارگرها می‌توانند همزمان کار کنند.  
در Rust، ماژول `std::thread` تمام ابزارهای لازم را در اختیارمان می‌گذارد. 🛠️

#### ۱۶.۱.۳. ایجاد ریسه با `thread::spawn`
برای ساختن یک ریسه‌ی جدید، از `thread::spawn` استفاده می‌کنیم. این تابع یک Closure (همان کوله‌پشتی جادویی فصل ۱۳) می‌گیرد و آن را در یک ریسه‌ی جداگانه اجرا می‌کند:
```rust
use std::thread;
use std::time::Duration;

fn main() {
    // استخدام یک کارگر جدید
    thread::spawn(|| {
        for i in 1..10 {
            println!("🐜 مورچه شماره {} دارد کار می‌کند", i);
            thread::sleep(Duration::from_millis(100)); // یک کم استراحت
        }
    });

    // ریسه اصلی هم کار خودش را می‌کند
    for i in 1..5 {
        println!("👑 ریسه اصلی: {}", i);
        thread::sleep(Duration::from_millis(50));
    }
}
```
`thread::sleep` باعث می‌شود ریسه برای چند میلی‌ثانیه بخوابد تا بتوانی ببینی چطور همزمان اجرا می‌شوند.

#### ۱۶.۱.۴. منتظر ماندن با `join`
اگر ریسه‌ی اصلی کارش زودتر تمام شود، ممکن است برنامه بسته شود و بقیه‌ی مورچه‌ها هم کارشان را نیمه‌کاره رها کنند! برای جلوگیری از این اتفاق، از `join` استفاده می‌کنیم. `join` یعنی: «صبر کن تا این ریسه کارش تمام شود، بعد برو مرحله‌ی بعد.»
```rust
let handle = thread::spawn(|| {
    println!("ریسه جدید شروع به کار کرد...");
    // کارهای طولانی
});

handle.join().unwrap(); // اینجا صبر می‌کنیم تا ریسه تمام شود
println!("همه کارها تمام شد!");
```

#### ۱۶.۱.۵. تمرین: دو ریسه همزمان
دو ریسه‌ی جداگانه بساز که هر کدام اعداد ۱ تا ۵ را با سرعت‌های متفاوت چاپ کنند. از `join` برای هر دو استفاده کن تا ریسه‌ی اصلی منتظر بماند.

💡 **پاسخ نمونه:**
```rust
use std::thread;
use std::time::Duration;

fn main() {
    let h1 = thread::spawn(|| {
        for i in 1..=5 {
            println!("🐜 مورچه ۱: {}", i);
            thread::sleep(Duration::from_millis(80));
        }
    });

    let h2 = thread::spawn(|| {
        for i in 1..=5 {
            println!("🐜 مورچه ۲: {}", i);
            thread::sleep(Duration::from_millis(50));
        }
    });

    h1.join().unwrap();
    h2.join().unwrap();
    println!("✅ همه مورچه‌ها کارشان را تمام کردند!");
}
```

![[Illustration: Cartoon illustration of a giant leaf being carried by a team of cute worker ants. One ant wears a crown labeled "Main Thread", others wear small hard hats labeled "Thread 1", "Thread 2". Above them, a progress bar fills up. Background: grassy field with soft sunlight. Style: vibrant children's book, educational metaphor, friendly characters, 16:9.]](../assets/images/16.1.png)

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> هم‌روندی یکی از پیشرفته‌ترین مباحث برنامه‌نویسی است. این فصل فقط مفاهیم پایه را معرفی می‌کند. اگر کودک در درک `Arc` یا `Mutex` مشکل داشت، نگران نباشید – این ابزارها در پروژه‌های حرفه‌ای استفاده می‌شوند و تسلط به زمان نیاز دارد. کتاب رسمی Rust فصل کاملی درباره‌ی هم‌روندی دارد:  
> [doc.rust-lang.org/book/ch16-00-concurrency.html](https://doc.rust-lang.org/book/ch16-00-concurrency.html)

---

### ۱۶.۲. انتقال داده بین ریسه‌ها

#### ۱۶.۲.۱. حرکت دادن مالکیت با `move`
مورچه‌ها برای اینکه بدانند برگ را به کدام سمت ببرند، باید با هم حرف بزنند. در Rust، وقتی یک Closure را به ریسه می‌دهیم، باید مالکیت متغیرهایش را به آن منتقل کنیم. این کار را با کلمه‌ی `move` انجام می‌دهیم:
```rust
let food = vec!["شکر", "نان", "عسل"];
let handle = thread::spawn(move || {
    println!("ریسه دارد غذاها را حمل می‌کند: {:?}", food);
});
handle.join().unwrap();
// println!("{:?}", food); // ❌ خطا! غذاها دیگر مال ریسه است
```
با `move`، ریسه مالک داده می‌شود و ریسه‌ی اصلی دیگر نمی‌تواند از آن استفاده کند.

#### ۱۶.۲.۲. کانال (mpsc) برای ارسال پیام
یک راه عالی برای حرف زدن ریسه‌ها، **کانال (Channel)** است. کانال مثل یک لوله‌ی زیرزمینی است که از یک طرف می‌توانی چیزی بیندازی در آن (فرستنده) و از طرف دیگر برداری (گیرنده).  
`mpsc` مخفف `multiple producer, single consumer` است. یعنی چند نفر می‌توانند پیام بفرستند، ولی فقط یک نفر گوش می‌دهد.
```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (tx, rx) = mpsc::channel(); // ساخت لوله‌ی ارتباطی

    thread::spawn(move || {
        let message = String::from("سلام از طرف مورچه!");
        tx.send(message).unwrap(); // انداختن در لوله
    });

    let received = rx.recv().unwrap(); // برداشتن از لوله
    println!("پیام دریافت شد: {}", received);
}
```
🔹 `tx` (فرستنده): می‌توانی `clone` بگیری و به چند ریسه بدهی.  
🔹 `rx` (گیرنده): متد `recv` منتظر می‌ماند تا پیام بیاید.

#### ۱۶.۲.۳. فرستادن چند پیام
می‌توانی چند پیام پشت سر هم بفرستی و در طرف مقابل با یک حلقه‌ی `for` همه‌شان را بگیری:
```rust
let (tx, rx) = mpsc::channel();
thread::spawn(move || {
    let messages = vec!["برو بالا", "برو پایین", "ایست!"];
    for msg in messages {
        tx.send(msg.to_string()).unwrap();
        thread::sleep(Duration::from_millis(200));
    }
});

for received in rx {
    println!("📢 دستور: {}", received);
}
```
حلقه‌ی `for` روی `rx` تا وقتی ادامه پیدا می‌کند که همه‌ی فرستنده‌ها بسته شوند.

#### ۱۶.۲.۴. دریافت غیرمسدود با `try_recv`
اگر نخواهی گیرنده منتظر بماند و بخواهی فوراً ببینی پیامی هست یا نه، از `try_recv` استفاده کن:
```rust
match rx.try_recv() {
    Ok(msg) => println!("پیام آمد: {}", msg),
    Err(_) => println!("هنوز پیامی نیامده، می‌روم سراغ کارهای دیگر..."),
}
```

#### ۱۶.۲.۵. تمرین: تولیدکننده و مصرف‌کننده
یک ریسه بساز که اعداد ۱ تا ۱۰ را از طریق کانال بفرستد. ریسه‌ی اصلی آن‌ها را دریافت کند و جمعشان را حساب کند.

💡 **پاسخ:**
```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || {
        for i in 1..=10 {
            tx.send(i).unwrap();
        }
    });

    let sum: i32 = rx.iter().sum();
    println!("مجموع اعداد: {}", sum); // ۵۵
}
```

![[Illustration: Cartoon underground pipe system connecting two ant hills. One hill has a sender ant dropping glowing message bottles into the pipe. The other hill has a receiver ant catching them. Labels "tx" and "rx" float above the hills. Style: playful educational vector, bright colors, clear technical metaphor, 16:9.]](../assets/images/16.2.png)

---

### ۱۶.۳. راهروی باریک (Mutex)

#### ۱۶.۳.۱. داستان: راهروی یک نفره
تصور کن چند مورچه می‌خواهند همزمان از یک راهروی خیلی باریک رد شوند. اگر همه با هم بروند، گیر می‌کنند! راه حل چیست؟ یک قفل دم در می‌گذارند. هر بار فقط یک مورچه می‌تواند وارد شود، قفل را می‌زند، کارش را انجام می‌دهد و موقع خروج قفل را باز می‌کند تا نفر بعدی بیاید.  
در برنامه‌نویسی، **Mutex** (مخفف Mutual Exclusion) دقیقاً همان قفل راهرو است.

#### ۱۶.۳.۲. Mutex<T> چیست؟
`Mutex<T>` یک جعبه‌ی هوشمند است که داده را قفل می‌کند. برای دسترسی به آن، اول باید `lock()` را صدا بزنی. وقتی کارت تمام شد، قفل خودکار باز می‌شود.
```rust
use std::sync::Mutex;

fn main() {
    let counter = Mutex::new(0);
    {
        let mut num = counter.lock().unwrap(); // گرفتن کلید قفل
        *num += 1; // تغییر مقدار
    } // کلید اینجا خودکار رها می‌شود
    println!("مقدار نهایی: {:?}", counter); // ۱
}
```

#### ۱۶.۳.۳. قفل کردن و دسترسی
اگر یک ریسه قفل را گرفته باشد و ریسه‌ی دیگری هم `lock()` بخواهد، آن ریسه‌ی دوم **مسدود** می‌شود و صبر می‌کند تا قفل آزاد شود. این‌طوری هیچ‌وقت دو ریسه همزمان یک چیز را تغییر نمی‌دهند و داده‌ها خراب نمی‌شوند. 🛡️

#### ۱۶.۳.۴. به اشتراک گذاری بین ریسه‌ها با `Arc`
برای اینکه چند ریسه بتوانند به یک `Mutex` دسترسی داشته باشند، باید مالکیتش را به اشتراک بگذارند. در فصل ۱۵ با `Rc` آشنا شدی که برای تک‌ریسه بود. برای چند ریسه، از پسرعموی امنش یعنی **`Arc`** (Atomic Reference Counting – شمارش ارجاع اتمی) استفاده می‌کنیم. `Arc` مخفف «شمارش ارجاع اتمی» است و در محیط چندریسه امن کار می‌کند.
```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0)); // دفترچه‌ی مشترک قفل‌دار
    let mut handles = vec![];

    for _ in 0..10 {
        let counter = Arc::clone(&counter); // یک کپی از اشاره‌گر
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap(); // گرفتن نوبت نوشتن
            *num += 1;
        });
        handles.push(handle);
    }

    for h in handles { h.join().unwrap(); }
    println!("نتیجه: {}", *counter.lock().unwrap()); // ۱۰
}
```
📌 **فرمول طلایی:** `Arc` = اشتراک مالکیت بین ریسه‌ها، `Mutex` = نوبت‌دهی برای نوشتن. ترکیبشان: `Arc<Mutex<T>>`!

#### ۱۶.۳.۵. تمرین: شمارنده‌ی اشتراکی
برنامه‌ای بنویس که ۱۰۰۰ ریسه بسازد. هر ریسه باید ۱۰۰۰ بار یک شمارنده‌ی مشترک را یکی زیاد کند. از `Arc<Mutex<u32>>` استفاده کن. در پایان، نتیجه باید دقیقاً ۱,۰۰۰,۰۰۰ باشد.

💡 **پاسخ نمونه:**
```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0));
    let mut handles = vec![];

    for _ in 0..1000 {
        let c = Arc::clone(&counter);
        let h = thread::spawn(move || {
            for _ in 0..1000 {
                let mut val = c.lock().unwrap();
                *val += 1;
            }
        });
        handles.push(h);
    }

    for h in handles { h.join().unwrap(); }
    println!("نتیجه نهایی: {}", *counter.lock().unwrap());
}
```

![[Illustration: A narrow cartoon hallway with a large padlock on the door. One ant holds a golden key labeled "Mutex Guard", walking inside. Other ants wait politely in line with numbered tickets. A glowing clipboard labeled "Arc" hangs on the wall. Style: clear educational metaphor, bright, friendly, children's book, 16:9.]](../assets/images/16.3.png)

---

### ۱۶.۴. پروژه: شمارشگر همزمان با ریسه‌ها

#### ۱۶.۴.۱. بدون Mutex: مسابقه داده (Data Race)
در Rust اگر بخواهی بدون `Mutex` یک داده را بین چند ریسه تغییر دهی، کامپایلر **اصلاً اجازه نمی‌دهد کد کامپایل شود!** مثلاً `Rc` برای چند ریسه امن نیست و اگر استفاده کنی، خطا می‌گیری.  
این یکی از قدرت‌های خارق‌العاده‌ی Rust است: **جلوی مسابقه‌ی داده (Data Race) را در زمان کامپایل می‌گیرد.** پس لازم نیست نگران باگ‌های عجیب و غریب باشی! 🛡️✨

#### ۱۶.۴.۲. با Mutex: راه‌حل درست
همان کد تمرین ۱۶.۳.۵ راه‌حل استاندارد و امن است. فقط کافی است `Arc::clone` را درست استفاده کنی و قبل از حلقه‌ی `join`، مطمئن شوی همه‌ی handleها ذخیره شده‌اند.

#### ۱۶.۴.۳. اجرا و مشاهده نتیجه
برنامه را چند بار اجرا کن. می‌بینی که همیشه دقیقاً `1000000` چاپ می‌شود. هیچ‌وقت عدد کم یا زیاد نمی‌شود. این یعنی Rust دارد عالی کار می‌کند! 🎉

![[Illustration: A split illustration. Left side: two ants trying to write on the same small notebook at the same time, causing a chaotic mess labeled "Data Race ❌". Right side: ants taking turns using a clipboard with a lock, result shows a perfect checkmark "1,000,000 ✅". Ferris stands in the middle giving a thumbs up. Style: educational vector, clear contrast, bright colors, 16:9.]](../assets/images/16.4.png)

---

### ۱۶.۵. جمع‌بندی و چالش

#### ۱۶.۵.۱. مرور مفاهیم
| مفهوم | کاربرد | ایموجی |
|-------|--------|--------|
| `thread::spawn` | ساخت یک ریسه‌ی جدید برای کار همزمان | 🧵 |
| `join` | صبر کردن تا تمام شدن کار ریسه | ⏳ |
| `move` | انتقال مالکیت متغیر به داخل ریسه | 🎒 |
| `mpsc::channel` | لوله‌ی ارتباطی امن بین ریسه‌ها | 📮 |
| `Mutex<T>` | قفل برای دسترسی نوبتی به داده | 🔒 |
| `Arc<T>` | اشتراک مالکیت امن بین چند ریسه | 🤝 |

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> هم‌روندی (مخصوصاً ترکیب `Arc` و `Mutex`) یکی از چالش‌برانگیزترین مباحث برنامه‌نویسی است. حتی برنامه‌نویسان حرفه‌ای هم گاهی در قفل‌ها و بن‌بست‌ها گیر می‌کنند. اگر هنوز همه‌چیز برایت روشن نیست، نگران نباش – با تمرین روی پروژه‌های کوچک، کمکم مسلط می‌شوی. مهم این است که بدانی Rust با ابزارهایش از تو در برابر وحشتناک‌ترین باگ‌های هم‌روندی محافظت می‌کند.

#### ۱۶.۵.۲. چالش: تولیدکننده-مصرف‌کننده با صف
یک برنامه بنویس که ۳ ریسه‌ی تولیدکننده بسازد. هر کدام ۱۰ عدد تصادفی تولید کنند و از طریق یک کانال مشترک بفرستند. ریسه‌ی اصلی (مصرف‌کننده) همه‌ی اعداد را جمع کند و نتیجه نهایی را چاپ کند.

💡 **راهنمایی:**  
- `tx` را قبل از شروع حلقه `clone` کن.  
- بعد از ساخته شدن همه‌ی ریسه‌ها، `tx` اصلی را `drop` کن تا کانال بسته شود و حلقه‌ی `rx` تمام شود.  
- **وابستگی `rand` را در `Cargo.toml` اضافه کن:**  
  ```toml
  [dependencies]
  rand = "0.9.0"
  ```

💡 **پاسخ نمونه:**
```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;
use rand::Rng;

fn main() {
    let (tx, rx) = mpsc::channel();
    let mut handles = vec![];

    for id in 0..3 {
        let tx_clone = tx.clone();
        let h = thread::spawn(move || {
            let mut rng = rand::thread_rng();
            for _ in 0..10 {
                let num = rng.gen_range(1..100);
                tx_clone.send(num).unwrap();
                thread::sleep(Duration::from_millis(10));
            }
        });
        handles.push(h);
    }

    drop(tx); // بستن فرستنده‌ی اصلی

    let sum: i32 = rx.iter().sum();
    println!("مجموع نهایی: {}", sum);

    for h in handles { h.join().unwrap(); }
}
```

حالا تو می‌دانی چطور از قدرت مورچه‌ها (ریسه‌ها) برای انجام چند کار همزمان استفاده کنی، چطور بینشان پیام بفرستی و چطور با قفل‌ها از داده‌هایت محافظت کنی. 🐜⚡  
در فصل بعد، می‌بینیم که Rust چطور مفاهیم شیءگرایی را به سبک منحصربه‌فرد خودش پیاده‌سازی می‌کند. آماده‌ای؟ 🦀✨

![[Illustration: Ferris wearing a graduation cap and safety goggles, holding a glowing "Chapter 16 Master" badge. Floating around him are thread spools, a channel pipe, a mutex lock, and an Arc clipboard. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/16.5.png)
