# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۱۳: قطار جادویی و کارخانه‌ی تبدیل (Iterators & Closures)

### 📑 فهرست فصل
[۱۳.۱. قطار باربری (Iterator)](#۱۳۱-قطار-باربری-iterator)  
[۱۳.۱.۱. داستان: قطار واگن‌های سنگ](#۱۳۱۱-داستان-قطار-واگن‌های-سنگ)  
[۱۳.۱.۲. Iterator چیست؟](#۱۳۱۲-iterator-چیست)  
[۱۳.۱.۳. گرفتن Iterator از یک Collection](#۱۳۱۳-گرفتن-iterator-از-یک-collection)  
[۱۳.۱.۴. متد next](#۱۳۱۴-متد-next)  
[۱۳.۱.۵. حلقه for و Iterator](#۱۳۱۵-حلقه-for-و-iterator)  
[۱۳.۱.۶. تمرین: پیمایش با while let](#۱۳۱۶-تمرین-پیمایش-با-while-let)  
[۱۳.۲. ماشین‌آلات کنار ریل (Adapter Methods)](#۱۳۲-ماشین‌آلات-کنار-ریل-adapter-methods)  
[۱۳.۲.۱. map: تبدیل هر عنصر](#۱۳۲۱-map-تبدیل-هر-عنصر)  
[۱۳.۲.۲. filter: انتخاب بر اساس شرط](#۱۳۲۲-filter-انتخاب-بر-اساس-شرط)  
[۱۳.۲.۳. زنجیره کردن (Chaining)](#۱۳۲۳-زنجیره-کردن-chaining)  
[۱۳.۲.۴. collect: جمع‌آوری نتایج](#۱۳۲۴-collect-جمع‌آوری-نتایج)  
[۱۳.۲.۵. سایر متدهای مفید (fold, any, all, sum)](#۱۳۲۵-سایر-متدهای-مفید-fold-any-all-sum)  
[۱۳.۲.۶. تمرین: اعداد زوج مجذور](#۱۳۲۶-تمرین-اعداد-زوج-مجذور)  
[۱۳.۳. کوله‌پشتی جاسوسی (Closures)](#۱۳۳-کوله‌پشتی-جاسوسی-closures)  
[۱۳.۳.۱. داستان: ابزار مخفی فریس](#۱۳۳۱-داستان-ابزار-مخفی-فریس)  
[۱۳.۳.۲. تعریف Closure](#۱۳۳۲-تعریف-closure)  
[۱۳.۳.۳. گرفتن متغیر از محیط](#۱۳۳۳-گرفتن-متغیر-از-محیط)  
[۱۳.۳.۴. انواع گرفتن (Fn, FnMut, FnOnce)](#۱۳۳۴-انواع-گرفتن-fn-fnmut-fnonce)  
[۱۳.۳.۵. حرکت دادن مالکیت با move](#۱۳۳۵-حرکت-دادن-مالکیت-با-move)  
[۱۳.۳.۶. تمرین: Closure ضرب‌کننده](#۱۳۳۶-تمرین-closure-ضرب‌کننده)  
[۱۳.۴. ترکیب Iterator و Closure](#۱۳۴-ترکیب-iterator-و-closure)  
[۱۳.۴.۱. map با Closure](#۱۳۴۱-map-با-closure)  
[۱۳.۴.۲. filter با Closure](#۱۳۴۲-filter-با-closure)  
[۱۳.۴.۳. مثال: خواندن خطوط از stdin و تبدیل به عدد](#۱۳۴۳-مثال-خواندن-خطوط-از-stdin-و-تبدیل-به-عدد)  
[۱۳.۴.۴. filter_map برای ترکیب دو کار](#۱۳۴۴-filter_map-برای-ترکیب-دو-کار)  
[۱۳.۵. پروژه: پردازش لاگ فایل](#۱۳۵-پروژه-پردازش-لاگ-فایل)  
[۱۳.۵.۱. ساختار خطوط لاگ](#۱۳۵۱-ساختار-خطوط-لاگ)  
[۱۳.۵.۲. خواندن فایل با Iterator](#۱۳۵۲-خواندن-فایل-با-iterator)  
[۱۳.۵.۳. فیلتر کردن خطوط ERROR](#۱۳۵۳-فیلتر-کردن-خطوط-error)  
[۱۳.۵.۴. شمارش خطاها با HashMap](#۱۳۵۴-شمارش-خطاها-با-hashmap)  
[۱۳.۶. جمع‌بندی و چالش](#۱۳۶-جمع‌بندی-و-چالش)  
[۱۳.۶.۱. مرور مفاهیم](#۱۳۶۱-مرور-مفاهیم)  
[۱۳.۶.۲. چالش: پیاده‌سازی Iterator برای فیبوناچی](#۱۳۶۲-چالش-پیاده‌سازی-iterator-برای-فیبوناچی)  

---

### ۱۳.۱. قطار باربری (Iterator)

#### ۱۳.۱.۱. داستان: قطار واگن‌های سنگ
فریس یک قطار باری بزرگ دارد که واگن‌هایش پر از سنگ‌های درخشان از سیاره‌های مختلف است. 🚂💎 او نمی‌خواهد همه‌ی سنگ‌ها را یکهو روی زمین خالی کند و زمین را شلوغ کند. ترجیح می‌دهد قطار آرام حرکت کند و هر بار فقط یک واگن باز شود و یک سنگ تحویل بدهد. به این کار می‌گویند **پیمایش (Iteration)**.  
در برنامه‌نویسی، وقتی با لیست‌ها یا مجموعه‌ها کار می‌کنیم، اغلب می‌خواهیم تک‌تک اعضای آن‌ها را ببینیم یا رویشان کار کنیم. ابزاری که این کار را برایمان راحت و مرتب انجام می‌دهد، **Iterator** (تکرارکننده) نام دارد.  
**اینجا داریم یاد می‌گیریم چطور بدون نوشتن حلقه‌های طولانی، روی داده‌ها پیمایش کنیم – یک گام بزرگ به سوی کدنویسی حرفه‌ای!** 🧙‍♂️

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> Iteratorها و Closureها از ویژگی‌های قدرتمند Rust هستند که نوشتن کدهای تمیز و کارآمد را ممکن می‌کنند. این فصل ممکن است برای بعضی کودکان چالش‌برانگیز باشد – نگران نباشید، در پروژه‌های بعدی بارها از آن‌ها استفاده خواهید کرد. کتاب رسمی Rust فصل کاملی درباره‌ی Iteratorها دارد:  
> [doc.rust-lang.org/book/ch13-00-functional-features.html](https://doc.rust-lang.org/book/ch13-00-functional-features.html)

#### ۱۳.۱.۲. Iterator چیست؟
Iterator یک موجود باهوش است که می‌داند چطور اعضای یک مجموعه را یکی یکی، به ترتیب، و فقط وقتی که ازش خواسته شود، تحویل بدهد. در Rust، Iterator یک `Trait` استاندارد دارد که مهم‌ترین ابزارش متد `next` است:
```rust
trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
}
```
🔹 هر بار `next` را صدا بزنی، عضو بعدی را داخل `Some(عضو)` به تو می‌دهد.  
🔹 وقتی دیگر عضوی باقی نمانده، `None` برمی‌گرداند.  
💡 **نکته‌ی طلایی:** Iteratorها **تنبل (Lazy)** هستند! یعنی تا وقتی ازشان نخواستی عضو بعدی را بدهند یا نتایج را جمع کنی، هیچ کاری انجام نمی‌دهند. این یعنی حافظه و سرعت را هدر نمی‌دهند! ⏱️

#### ۱۳.۱.۳. گرفتن Iterator از یک Collection
برای اینکه از یک وکتور یا آرایه Iterator بگیری، سه راه اصلی داری:

| متد | نوع خروجی | توضیح ساده |
|-----|-----------|------------|
| `.iter()` | `&T` | فقط **نگاه** می‌کند (قرض غیرقابل تغییر). خود مجموعه دست‌نخورده می‌ماند. |
| `.iter_mut()` | `&mut T` | نگاه می‌کند و **اجازه تغییر** می‌دهد. |
| `.into_iter()` | `T` | **مالکیت** را می‌گیرد. بعد از تمام شدن، دیگر نمی‌توانی از مجموعه استفاده کنی. |

```rust
let v = vec![10, 20, 30];

let iter1 = v.iter();       // فقط نگاه می‌کند
let iter2 = v.iter_mut();   // می‌تواند تغییر بدهد
let iter3 = v.into_iter();  // مالکیت را می‌گیرد (v بعد از این خط دیگر قابل استفاده نیست)
```

#### ۱۳.۱.۴. متد `next`
می‌توانی دستی `next` را صدا بزنی و ببینی چطور کار می‌کند:
```rust
let v = vec!["سیب", "موز", "پرتقال"];
let mut iter = v.iter(); // باید mut باشد چون موقعیت داخلی‌اش عوض می‌شود

assert_eq!(iter.next(), Some(&"سیب"));
assert_eq!(iter.next(), Some(&"موز"));
assert_eq!(iter.next(), Some(&"پرتقال"));
assert_eq!(iter.next(), None); // دیگر چیزی نمانده!
```

#### ۱۳.۱.۵. حلقه `for` و Iterator
خبر خوب این است که لازم نیست خودت درگیر `next` شوی! حلقه‌ی `for` در Rust خودش پشت صحنه Iterator می‌سازد و تا وقتی `None` برنگرداند، حلقه را ادامه می‌دهد:
```rust
let names = vec!["فریس", "بیل", "لونا"];
for name in &names {   // &names دقیقاً همان names.iter() است
    println!("سلام {}!", name);
}
```
⚠️ اگر بنویسی `for name in names` (بدون `&`)، حلقه مالکیت `names` را می‌گیرد و بعد از حلقه دیگر نمی‌توانی از آن استفاده کنی.

#### ۱۳.۱.۶. تمرین: پیمایش با `while let`
با استفاده از `while let` و `next()`، وکتور `["الف", "ب", "ج"]` را پیمایش کن و هر کدام را چاپ کن.

💡 **پاسخ:**
```rust
fn main() {
    let v = vec!["الف", "ب", "ج"];
    let mut iter = v.iter();
    
    while let Some(item) = iter.next() {
        println!("{}", item);
    }
}
```
`while let` یعنی: «تا وقتی `next` مقدار `Some` می‌دهد، کد را اجرا کن. وقتی `None` شد، خودکار متوقف شو.» خیلی تمیز است! ✨

![[Illustration: A friendly cartoon crab (Ferris) standing on a platform next to a colorful train. Each train car has a glowing gem inside. A conveyor arm lifts one gem at a time as the train moves slowly. Background: starry sky with a control panel showing "next() → Some(gem)". Style: vibrant children's book illustration, playful tech metaphor, soft lighting, 16:9.]](../assets/images/13.1.png)

---

### ۱۳.۲. ماشین‌آلات کنار ریل (Adapter Methods)

#### ۱۳.۲.۱. `map`: تبدیل هر عنصر
در مسیر قطار، ماشین‌هایی هستند که سنگ‌ها را می‌گیرند، شکل یا رنگشان را عوض می‌کنند و به واگن بعدی می‌فرستند. در Rust به این‌ها **Adapter** می‌گوییم. معروف‌ترینشان `map` است. یک Closure می‌گیرد و روی هر عنصر اعمالش می‌کند:
```rust
let numbers = vec![1, 2, 3];
let doubled: Vec<_> = numbers.iter().map(|x| x * 2).collect();
println!("{:?}", doubled); // [2, 4, 6]
```
⚠️ **دقت کن:** `map` به تنهایی هیچ کاری نمی‌کند! فقط یک Iterator جدید می‌سازد که می‌گوید: «وقتی ازم خواستند، این تبدیل را انجام می‌دهم.»

#### ۱۳.۲.۲. `filter`: انتخاب بر اساس شرط
یک ماشین دیگر هم هست که فقط سنگ‌هایی را رد می‌کند که یک شرط خاص را داشته باشند. اگر شرط `true` باشد، سنگ رد می‌شود؛ اگر `false` باشد، از ریل خارج می‌شود. برای راحت‌تر کردن کار با مرجع‌ها، از `.copied()` استفاده می‌کنیم:
```rust
let numbers = vec![1, 2, 3, 4, 5];
let evens: Vec<i32> = numbers.iter().copied().filter(|&x| x % 2 == 0).collect();
println!("{:?}", evens); // [2, 4]
```
`.copied()` باعث می‌شود به جای `&i32` از `i32` واقعی استفاده کنیم. این‌طوری مجبور نیستیم با `|&&x|` کار کنیم.

#### ۱۳.۲.۳. زنجیره کردن (Chaining)
زیبایی Iteratorها اینجاست که می‌توانی ماشین‌ها را پشت سر هم بچینی:
```rust
let numbers = vec![1, 2, 3, 4, 5];
let result: Vec<_> = numbers.iter()
    .copied()
    .filter(|&x| x % 2 == 0)   // اول فقط زوج‌ها را جدا کن
    .map(|x| x * 10)           // بعد ضربدر ۱۰ کن
    .collect();                // در نهایت جمعشان کن
println!("{:?}", result); // [20, 40]
```
این زنجیره تا وقتی به `.collect()` یا `.sum()` نرسد، **هیچ محاسبه‌ای انجام نمی‌دهد**. Rust آن‌قدر باهوش است که می‌فهمد چطور کارها را بهینه انجام بدهد! 🧠⚡

#### ۱۳.۲.۴. `collect`: جمع‌آوری نتایج
`collect` آخرین ایستگاه است. Iterator را می‌گیرد و همه‌ی نتایج را در یک Collection جدید (مثل `Vec` یا `HashMap`) می‌ریزد. معمولاً باید نوعش را مشخص کنی: `Vec<_>` یا `::<Vec<i32>>`.

#### ۱۳.۲.۵. سایر متدهای مفید
| متد | کاربرد | مثال |
|-----|--------|------|
| `sum()` | جمع اعداد | `numbers.iter().sum::<i32>()` |
| `fold(init, \|acc, x\| ...)` | جمع‌کننده‌ی عمومی | `fold(0, \|acc, x\| acc + x)` |
| `any(\|&x\| ...)` | حداقل یکی شرط را دارد؟ | `any(\|&x\| x > 10)` |
| `all(\|&x\| ...)` | همه شرط را دارند؟ | `all(\|&x\| x > 0)` |

#### ۱۳.۲.۶. تمرین: اعداد زوج مجذور
یک وکتور از اعداد ۱ تا ۱۰ بساز. با `filter` و `map`، فقط زوج‌ها را انتخاب کن، مربعشان را حساب کن، و در یک وکتور جدید جمع کن.

💡 **پاسخ:**
```rust
fn main() {
    let result: Vec<i32> = (1..=10)
        .filter(|&x| x % 2 == 0)
        .map(|x| x * x)
        .collect();
    println!("{:?}", result); // [4, 16, 36, 64, 100]
}
```
`(1..=10)` خودش یک Range است و Iterator را پیاده‌سازی می‌کند. نیازی به `vec!` نیست!

![[Illustration: A cartoon factory conveyor belt with labeled machines: "filter", "map", "collect". Glowing cubes travel through, changing shape and color at each station. Ferris operates a control panel with a big green "Run" button. Style: educational vector, bright, clean, 16:9.]](../assets/images/13.2.png)

---

### ۱۳.۳. کوله‌پشتی جاسوسی (Closures)

#### ۱۳.۳.۱. داستان: ابزار مخفی فریس
فریس یک کوله‌پشتی جادویی دارد که می‌تواند یک عملیات مخفی را در خودش ذخیره کند. مثلاً به آن می‌گوید: «هر عددی به تو دادم، ضربدر ۳ کن.» بعداً هر وقت فریس بخواهد، کوله‌پشتی آن کار را انجام می‌دهد. جادوی اصلی اینجاست که کوله‌پشتی می‌تواند **چیزهایی را از محیط اطرافش به خاطر بسپارد**. در Rust به این ابزار **Closure** (بستار) می‌گوییم. 🎒✨

#### ۱۳.۳.۲. تعریف Closure
نحو Closure خیلی ساده است: `|پارامترها| { بدنه }`. اگر بدنه فقط یک خط باشد، آکولاد `{}` لازم نیست:
```rust
let add_one = |x| x + 1;
println!("{}", add_one(5)); // 6

let multiply = |a, b| a * b;
println!("{}", multiply(4, 5)); // 20
```
نوع پارامترها و خروجی معمولاً توسط کامپایلر خودش حدس زده می‌شود.

#### ۱۳.۳.۳. گرفتن متغیر از محیط
Closure می‌تواند از متغیرهایی که بیرون از خودش تعریف شده‌اند استفاده کند:
```rust
let factor = 3;
let multiply_by_factor = |x| x * factor; // factor را از محیط می‌گیرد
println!("{}", multiply_by_factor(10)); // 30
```
اما Closure با این متغیرها چطور رفتار می‌کند؟ سه حالت دارد که کامپایلر خودش انتخاب می‌کند:

#### ۱۳.۳.۴. انواع گرفتن (Fn, FnMut, FnOnce)
| نوع | رفتار | مثال |
|-----|--------|------|
| `Fn` | فقط **می‌خواند** (قرض معمولی `&`). چند بار می‌توانی صدایش بزنی. | `|x| x + factor` |
| `FnMut` | می‌تواند **تغییر بدهد** (قرض mutable `&mut`). چند بار صدا زده می‌شود. | `|| { count += 1; count }` |
| `FnOnce` | **مالکیت را می‌گیرد** و مصرف می‌کند. فقط **یک بار** می‌توانی صدایش بزنی. | `|| println!("{}", s)` وقتی `s` کپی نمی‌شود. |

مثال `FnMut`:
```rust
let mut count = 0;
let mut increment = || {
    count += 1;
    count
};
println!("{}", increment()); // 1
println!("{}", increment()); // 2
```

#### ۱۳.۳.۵. حرکت دادن مالکیت با `move`
اگر قبل از Closure کلمه‌ی `move` را بگذاری، به Closure می‌گویی: «لطفاً مالکیت متغیرهای محیط را کامل به خودت منتقل کن.» این زمانی کاربرد دارد که بخواهی Closure را به یک ریسه (Thread) دیگر بفرستی:
```rust
let s = String::from("سلام فضایی");
let consume = move || {
    println!("{}", s);
};
consume();
// println!("{}", s); // ❌ خطا! مالکیت رفته پیش consume
```

#### ۱۳.۳.۶. تمرین: Closure ضرب‌کننده
تابعی به اسم `make_multiplier` بنویس که یک عدد `factor` بگیرد و یک Closure برگرداند. Closure باید هر عددی که به آن داده می‌شود را در `factor` ضرب کند. از `move` استفاده کن.

💡 **پاسخ:**
```rust
fn make_multiplier(factor: i32) -> impl Fn(i32) -> i32 {
    move |x| x * factor
}

fn main() {
    let double = make_multiplier(2);
    let triple = make_multiplier(3);
    println!("{}", double(5));  // 10
    println!("{}", triple(5));  // 15
}
```

![[Illustration: A cartoon crab wearing a futuristic backpack with glowing memory chips. Around the crab float variables like "factor = 3" and "x" being pulled into the backpack. A "move" tag is stamped on the backpack. Style: playful sci-fi educational, bright colors, 16:9.]](../assets/images/13.3.png)

---

### ۱۳.۴. ترکیب Iterator و Closure

#### ۱۳.۴.۱. `map` با Closure
Adapterهایی مثل `map` و `filter` دقیقاً همان Closureها را به عنوان ورودی می‌گیرند:
```rust
let names = vec!["فریس", "بیل"];
let greetings: Vec<_> = names.iter()
    .map(|name| format!("سلام {}!", name))
    .collect();
println!("{:?}", greetings); // ["سلام فریس!", "سلام بیل!"]
```

#### ۱۳.۴.۲. `filter` با Closure
```rust
let numbers = vec![5, 15, 25, 8];
let big_numbers: Vec<_> = numbers.iter()
    .copied()
    .filter(|&x| x > 10)
    .collect();
println!("{:?}", big_numbers); // [15, 25]
```

#### ۱۳.۴.۳. مثال: خواندن خطوط از stdin و تبدیل به عدد
فرض کن کاربر چند عدد را خط به خط وارد می‌کند و می‌خواهیم جمعشان را حساب کنیم:
```rust
use std::io::{self, BufRead};

fn main() {
    let stdin = io::stdin();
    let sum: i32 = stdin.lock().lines()
        .map(|line| line.unwrap().trim().parse::<i32>().unwrap())
        .sum();
    println!("مجموع: {}", sum);
}
```
اینجا `stdin.lock().lines()` یک Iterator از خطوط می‌دهد. `map` هر خط را می‌گیرد، تمیز می‌کند و به عدد تبدیل می‌کند. در نهایت `sum()` همه را جمع می‌کند.

#### ۱۳.۴.۴. `filter_map` برای ترکیب دو کار
گاهی می‌خواهیم همزمان **تبدیل** کنیم و **فیلتر**. `filter_map` یک Closure می‌گیرد که `Option<T>` برمی‌گرداند. اگر `Some` باشد، نگهش می‌دارد؛ اگر `None` باشد، دور می‌اندازد:
```rust
let strings = vec!["3", "seven", "8", "10"];
let numbers: Vec<i32> = strings.iter()
    .filter_map(|s| s.parse().ok()) // اگر parse نشود، None می‌دهد و حذف می‌شود
    .collect();
println!("{:?}", numbers); // [3, 8, 10]
```
`.ok()` یک متد کمکی است که `Result` را به `Option` تبدیل می‌کند. خیلی برای پاک‌سازی داده‌ها کاربرد دارد! 🧼

![[Illustration: A cartoon sorting machine with a "filter_map" label. As items pass through, some are converted and drop into a "Collected" box while invalid items slide into a "Rejected" bin. Ferris watches the process. Style: educational, playful, bright colors, 16:9.]](../assets/images/13.4.png)

---

### ۱۳.۵. پروژه: پردازش لاگ فایل

حالا وقتش است همه‌ی اینها را در یک پروژه‌ی واقعی بگذاریم. فرض کن یک فایل `log.txt` داری که وضعیت سیستم را ثبت کرده:
```text
INFO: سیستم راه‌اندازی شد
ERROR: دیسک پر است
WARNING: حافظه رو به اتمام
ERROR: اتصال شبکه قطع شد
INFO: کار تمام شد
```
می‌خواهیم خطوط `ERROR` را پیدا کنیم و ببینیم هر کدام چند بار تکرار شده‌اند.

#### ۱۳.۵.۱. ساختار خطوط لاگ
هر خط با یک برچسب مثل `ERROR:` شروع می‌شود. ما فقط به خطاهای واقعی کار داریم.

#### ۱۳.۵.۲. خواندن فایل با Iterator
```rust
use std::fs::File;
use std::io::{BufRead, BufReader};

fn main() {
    let file = File::open("log.txt").expect("فایل log.txt پیدا نشد");
    let reader = BufReader::new(file);
    // ... ادامه کد
}
```

#### ۱۳.۵.۳. فیلتر کردن خطوط ERROR
```rust
let error_lines: Vec<String> = reader.lines()
    .filter_map(|line| line.ok()) // اگر خطایی در خواندن فایل پیش آمد، نادیده بگیر
    .filter(|line| line.starts_with("ERROR"))
    .collect();

println!("خطاهای پیدا شده:");
for line in &error_lines {
    println!("  {}", line);
}
```

#### ۱۳.۵.۴. شمارش خطاها با HashMap
حالا بیاییم ببینیم هر خطا چند بار تکرار شده:
```rust
use std::collections::HashMap;

let mut counts = HashMap::new();
for line in reader.lines().filter_map(|l| l.ok()) {
    if let Some(msg) = line.strip_prefix("ERROR: ") {
        *counts.entry(msg.to_string()).or_insert(0) += 1;
    }
}

println!("\n📊 آمار خطاها:");
for (msg, count) in &counts {
    println!("  - {} : {} بار", msg, count);
}
```
`strip_prefix` فقط اگر خط با `"ERROR: "` شروع شود، بقیه‌ی متن را برمی‌گرداند. بعد با `entry` و `or_insert` تعدادش را می‌شماریم. کدی که هم تمیز است، هم سریع! ⚡

![[Illustration: A cartoon control desk with a scrolling screen of log lines. A glowing filter machine catches only "ERROR" tags and drops them into a counting jar. Ferris adjusts a dial labeled "filter_map". Style: cozy tech workspace, educational vector, warm lighting, 16:9.]](../assets/images/13.5.png)

---

### ۱۳.۶. جمع‌بندی و چالش

#### ۱۳.۶.۱. مرور مفاهیم
در این فصل یاد گرفتی:  
✅ **Iterator**: شیء برای پیمایش مرحله‌ای مجموعه‌ها. متد اصلی `next`.  
✅ **`.iter()` / `.iter_mut()` / `.into_iter()`**: راه‌های گرفتن Iterator با سطوح دسترسی مختلف.  
✅ **Adapterها**: `map` (تبدیل)، `filter` (انتخاب)، `collect` (جمع‌بندی)، `fold`/`sum`/`any`/`all`. همه‌ی اینها **تنبل (Lazy)** هستند.  
✅ **Closure**: تابع بی‌نام که متغیرهای محیط را می‌گیرد. نحو `|x| x * 2`.  
✅ **انواع Closure**: `Fn` (فقط خواندن)، `FnMut` (تغییر)، `FnOnce` (مصرف کردن).  
✅ **`move`**: انتقال مالکیت متغیرهای محیط به داخل Closure.  
✅ **`filter_map`**: ترکیب هوشمندانه‌ی فیلتر و تبدیل.  
✅ **این ابزارها تو را قادر می‌سازند کدهای کوتاه، سریع و شبیه به زبان انسان بنویسی – مانند یک جادوگر واقعی!** 🧙

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> Closureها و Iteratorهای زنجیره‌ای ممکن است در ابتدا گیج‌کننده به نظر برسند. حتی برنامه‌نویسان حرفه‌ای هم گاهی برای نوشتن یک زنجیره‌ی پیچیده چند بار تلاش می‌کنند. نگران نباش – با تمرین، این ابزارها برایت طبیعی می‌شوند و نوشتن کدهای زیبا را برایت لذت‌بخش می‌کنند.

#### ۱۳.۶.۲. چالش: پیاده‌سازی Iterator برای فیبوناچی
یک `struct` به اسم `Fibonacci` بساز که `Iterator` را پیاده‌سازی کند. هر بار که `next` صدا زده می‌شود، عدد بعدی دنباله (۰, ۱, ۱, ۲, ۳, ۵, ۸, ...) را برگرداند. سپس با `.take(10)` ده عدد اول را چاپ کن.

💡 **پاسخ نمونه:**
```rust
struct Fibonacci {
    current: u64,
    next: u64,
}

impl Fibonacci {
    fn new() -> Self {
        Fibonacci { current: 0, next: 1 }
    }
}

impl Iterator for Fibonacci {
    type Item = u64;

    fn next(&mut self) -> Option<Self::Item> {
        let new_next = self.current + self.next;
        let result = self.current;
        self.current = self.next;
        self.next = new_next;
        Some(result)
    }
}

fn main() {
    let fib = Fibonacci::new();
    for num in fib.take(10) {
        println!("{}", num);
    }
}
```
`take(10)` خودش یک Adapter دیگر است که فقط ۱۰ عضو اول Iterator را برمی‌گرداند. ترکیب `struct + Trait + Adapter` دقیقاً همان جایی است که Rust می‌درخشد! 🌟

حالا تو می‌دانی چطور با Iteratorها و Closureها کدهای خواناتر، کوتاه‌تر و حرفه‌ای‌تر بنویسی. در فصل بعد، سری به **سوپرمارکت بزرگ Rust (Crates.io)** می‌زنیم و یاد می‌گیریم چطور از کتابخانه‌های آماده‌ی دیگران استفاده کنیم تا برنامه‌های قدرتمندتری بسازیم. 📦🚀

