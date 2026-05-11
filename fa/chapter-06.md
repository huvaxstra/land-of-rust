# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۶: ماشین انتخاب لباس (Enums و Match)

### 📑 فهرست فصل
[۶.۱. امروز هوا چطوره؟ (Enum)](#۶۱-امروز-هوا-چطوره-enum)  
[۶.۱.۱. داستان: کمد لباس هوشمند فریس](#۶۱۱-داستان-کمد-لباس-هوشمند-فریس)  
[۶.۱.۲. مشکل: عدد یا رشته؟](#۶۱۲-مشکل-عدد-یا-رشته)  
[۶.۱.۳. تعریف enum با حالت‌های مختلف](#۶۱۳-تعریف-enum-با-حالت‌های-مختلف)  
[۶.۱.۴. ساختن مقدار از enum](#۶۱۴-ساختن-مقدار-از-enum)  
[۶.۲. یک کمد پر از لباس (Enum with Data)](#۶۲-یک-کمد-پر-از-لباس-enum-with-data)  
[۶.۲.۱. هر حالت می‌تواند داده‌ی متفاوتی داشته باشد](#۶۲۱-هر-حالت-می‌تواند-دادهی-متفاوتی-داشته-باشد)  
[۶.۲.۲. تعریف enum با داده](#۶۲۲-تعریف-enum-با-داده)  
[۶.۲.۳. ساختن نمونه از enum با داده](#۶۲۳-ساختن-نمونه-از-enum-با-داده)  
[۶.۲.۴. تفاوت enum با struct](#۶۲۴-تفاوت-enum-با-struct)  
[۶.۳. کیف گمشده (Option)](#۶۳-کیف-گمشده-option)  
[۶.۳.۱. داستان: دنبال کلید سفینه](#۶۳۱-داستان-دنبال-کلید-سفینه)  
[۶.۳.۲. معرفی Option](#۶۳۲-معرفی-option)  
[۶.۳.۳. استفاده از Some و None](#۶۳۳-استفاده-از-some-و-none)  
[۶.۳.۴. چرا Option بهتر از null است؟](#۶۳۴-چرا-option-بهتر-از-null-است)  
[۶.۳.۵. متدهای مفید روی Option](#۶۳۵-متدهای-مفید-روی-option)  
[۶.۳.۶. تمرین: تابع safe_divide](#۶۳۶-تمرین-تابع-safe_divide)  
[۶.۴. ریموت کنترل هوشمند (Match)](#۶۴-ریموت-کنترل-هوشمند-match)  
[۶.۴.۱. مشکل: چطور بر اساس مقدار enum تصمیم بگیریم؟](#۶۴۱-مشکل-چطور-بر-اساس-مقدار-enum-تصمیم-بگیریم)  
[۶.۴.۲. معرفی match](#۶۴۲-معرفی-match)  
[۶.۴.۳. شرط exhaustive (همه حالت‌ها باید پوشش داده شوند)](#۶۴۳-شرط-exhaustive-همه-حالت‌ها-باید-پوشش-داده-شوند)  
[۶.۴.۴. استخراج داده از enum با match](#۶۴۴-استخراج-داده-از-enum-با-match)  
[۶.۴.۵. الگوی catch-all با _](#۶۴۵-الگوی-catch-all-با-_)  
[۶.۴.۶. match با Option](#۶۴۶-match-با-option)  
[۶.۴.۷. if let برای ساده‌تر شدن](#۶۴۷-if-let-برای-ساده‌تر-شدن)  
[۶.۴.۸. تمرین: ارزش سکه‌ها](#۶۴۸-تمرین-ارزش-سکه‌ها)  
[۶.۵. پروژه: ماشین لباسشویی هوشمند](#۶۵-پروژه-ماشین-لباسشویی-هوشمند)  
[۶.۵.۱. تعریف enum برای آب و هوا](#۶۵۱-تعریف-enum-برای-آب-و-هوا)  
[۶.۵.۲. تابع پیشنهاد لباس](#۶۵۲-تابع-پیشنهاد-لباس)  
[۶.۵.۳. گرفتن ورودی از کاربر](#۶۵۳-گرفتن-ورودی-از-کاربر)  
[۶.۵.۴. استفاده از Option برای رنگ دلخواه](#۶۵۴-استفاده-از-option-برای-رنگ-دلخواه)  
[۶.۶. جمع‌بندی و چالش](#۶۶-جمع‌بندی-و-چالش)  
[۶.۶.۱. مرور مفاهیم](#۶۶۱-مرور-مفاهیم)  
[۶.۶.۲. چالش: ماشین حساب با Result](#۶۶۲-چالش-ماشین-حساب-با-result)  

---

### ۶.۱. امروز هوا چطوره؟ (Enum)

#### ۶.۱.۱. داستان: کمد لباس هوشمند فریس
فریس یک کمد لباس جادویی دارد که می‌تواند بر اساس وضعیت آب و هوا بهش بگوید چه لباسی بپوشد. اما آب و هوا فقط یک حالت نیست؛ می‌تواند آفتابی، بارونی، برفی یا ابری باشد. فریس می‌خواهد در برنامه‌اش این چهار حالت را ذخیره کند. به جای اینکه از عدد یا متن ساده استفاده کند (که ممکن است اشتباه تایپی پیش بیاید)، Rust یک ابزار عالی به اسم `enum` دارد.  
**این یعنی کامپیوتر می‌تواند مثل انسان‌ها در دسته‌ها فکر کند – گامی دیگر به سوی جادوگر کامپیوتر شدن!** 🧙‍♂️

#### ۶.۱.۲. مشکل: عدد یا رشته؟
فرض کن می‌خواستیم با عدد کار کنیم:
```rust
let weather = 1; // ۱ یعنی آفتابی، ۲ یعنی بارانی، ...
```
اما اگر اشتباهی عدد ۵ را بگذاریم چه؟ یا با متن:
```rust
let weather = "sunny";
```
اگر `"suny"` تایپ کنیم (یک حرف جا بندازیم)، برنامه گیج می‌شود! `enum` این مشکل را حل می‌کند. فقط اجازه می‌دهد از یک لیست مشخص انتخاب کنی. هیچ چیز دیگری مجاز نیست.

#### ۶.۱.۳. تعریف enum با حالت‌های مختلف
با کلمه‌ی کلیدی `enum` یک نوع جدید می‌سازیم که فقط می‌تواند یکی از چند مقدار مشخص را داشته باشد:
```rust
enum Weather {
    Sunny,
    Rainy,
    Snowy,
    Cloudy,
}
```
حالا `Weather` یک نوع داده‌ی جدید شده، درست مثل `i32` یا `String`. اما فقط چهار مقدار مجاز دارد.

#### ۶.۱.۴. ساختن مقدار از enum
برای ساختن یک مقدار از این enum، اسم enum را می‌نویسیم، بعد دو تا دونقطه (`::`) و سپس حالت مورد نظر:
```rust
let today = Weather::Sunny;
let tomorrow = Weather::Rainy;
```
`::` یعنی «از داخل این enum، آن حالت خاص را انتخاب کن».

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> Enumها (شمارنده‌ها) یکی از مفاهیم خوش‌ساخت Rust هستند که به کودکان کمک می‌کنند تا «دسته‌بندی» را در برنامه‌نویسی بفهمند. کتاب رسمی Rust فصل کاملی درباره‌ی enumها دارد:  
> [doc.rust-lang.org/book/ch06-00-enums.html](https://doc.rust-lang.org/book/ch06-00-enums.html)

![[Illustration: Cartoon illustration of Ferris the crab standing in front of a magical weather map. Four glowing icons float above: sun, rain cloud, snowflake, and gray cloud. A friendly "enum" selector tool connects them to a dropdown menu. Style: vibrant children's book illustration, clear educational metaphor, soft lighting, 16:9.]](../assets/images/6.1.png)

---

### ۶.۲. یک کمد پر از لباس (Enum with Data)

#### ۶.۲.۱. هر حالت می‌تواند داده‌ی متفاوتی داشته باشد
همه‌ی روزهای آفتابی یک‌جور نیستند. گاهی هوا ۲۵ درجه است، گاهی ۳۵ درجه. برای روزهای بارونی شاید بخواهیم رنگ چتر را هم بدانیم. enum در Rust می‌تواند برای هر حالت، داده‌ی اضافی نگه دارد!

#### ۶.۲.۲. تعریف enum با داده
```rust
enum WeatherInfo {
    Sunny { temperature: u8 },
    Rainy { umbrella_color: String },
    Snowy { scarf_material: String },
    Cloudy,
}
```
🔹 `Sunny` یک فیلد به اسم `temperature` از نوع `u8` دارد.  
🔹 `Rainy` یک فیلد `umbrella_color` از نوع `String` دارد.  
🔹 `Snowy` یک فیلد `scarf_material` از نوع `String` دارد.  
🔹 `Cloudy` هیچ داده‌ی اضافی‌ای ندارد.

#### ۶.۲.۳. ساختن نمونه از enum با داده
```rust
let sunny_day = WeatherInfo::Sunny { temperature: 32 };
let rainy_day = WeatherInfo::Rainy { umbrella_color: String::from("قرمز") };
let snowy_day = WeatherInfo::Snowy { scarf_material: String::from("پشمی") };
let cloudy_day = WeatherInfo::Cloudy;
```

#### ۶.۲.۴. تفاوت enum با struct
🔹 **struct:** همه‌ی فیلدها همیشه وجود دارند. مثلاً یک `Monster` همیشه اسم، رنگ، پا و قدرت دارد.  
🔹 **enum:** فقط **یکی** از حالت‌ها انتخاب می‌شود. یک `WeatherInfo` یا آفتابی است یا بارونی یا برفی یا ابری. نمی‌تواند همزمان هم دما داشته باشد هم رنگ چتر!

![[Illustration: Split educational graphic. Left side: a "struct" box showing all four slots filled at once. Right side: an "enum" wardrobe with four drawers, but only ONE drawer is open at a time. Ferris points to the open drawer explaining the difference. Style: clean, cartoon, bright colors, clear visual metaphor, 16:9.]](../assets/images/6.2.png)

---

### ۶.۳. کیف گمشده (Option)

#### ۶.۳.۱. داستان: دنبال کلید سفینه
فریس همیشه کلید سفینه‌اش را در کیفش می‌گذارد. اما بعضی روزها یادش می‌رود و کیف خالی است! در برنامه‌نویسی، ما به این موقعیت می‌گوییم «ممکن است چیزی وجود داشته باشد یا نداشته باشد». در خیلی از زبان‌ها از `null` استفاده می‌کنند، اما `null` خیلی خطرناک است و باعث کرش برنامه می‌شود. Rust اصلاً `null` ندارد؛ به جایش از `Option` استفاده می‌کند.

#### ۶.۳.۲. معرفی `Option<T>`
`Option` یک enum بسیار پرکاربرد است که در کتابخانه‌ی استاندارد Rust تعریف شده:
```rust
enum Option<T> {
    Some(T),
    None,
}
```
`T` یعنی «هر نوعی می‌تواند اینجا قرار بگیرد». `Some(T)` یعنی «یک چیز از نوع T داریم»، و `None` یعنی «هیچی نداریم».

#### ۶.۳.۳. استفاده از `Some` و `None`
```rust
let key = Some(String::from("کلید طلایی")); // کلید هست
let no_key: Option<String> = None;          // کلید نیست
```
اگر فقط `None` بنویسی، باید به کامپایلر بگویی که چه نوعی را انتظار داری (مثلاً `Option<String>`).

#### ۶.۳.۴. چرا Option بهتر از null است؟
در زبان‌هایی که `null` دارند، اگر فراموش کنی چک کنی چیزی `null` هست یا نه، برنامه ممکن است یکهو بترکد. اما در Rust، کامپایلر مجبورت می‌کند هر دو حالت `Some` و `None` را بررسی کنی. این‌طوری برنامه‌ات خیلی امن‌تر می‌شود! 🛡️

#### ۶.۳.۵. متدهای مفید روی Option
🔹 `.unwrap()`: اگر `Some` بود مقدار درونش را می‌دهد، اگر `None` بود برنامه را متوقف می‌کند. (فقط وقتی ۱۰۰٪ مطمئنی خالی نیست استفاده کن!)  
🔹 `.unwrap_or(default)`: اگر `None` بود، یک مقدار پیش‌فرض برمی‌گرداند.  
🔹 `.is_some()` / `.is_none()`: چک می‌کند مقدار هست یا نه.

```rust
let key = Some(String::from("abc"));
let value = key.unwrap_or(String::from("کلید پیدا نشد"));
println!("{}", value); // abc
```

#### ۶.۳.۶. تمرین: تابع `safe_divide`
یک تابع به اسم `safe_divide` بنویس که دو عدد اعشاری (`f64`) بگیرد. اگر عدد دوم صفر نبود، حاصل تقسیم را درون `Some` برگرداند، در غیر این صورت `None` برگرداند.

💡 **پاسخ:**
```rust
fn safe_divide(a: f64, b: f64) -> Option<f64> {
    if b == 0.0 {
        None
    } else {
        Some(a / b)
    }
}

fn main() {
    let result = safe_divide(10.0, 2.0);
    match result {
        Some(r) => println!("نتیجه: {}", r),
        None => println!("خطا: تقسیم بر صفر"),
    }
}
```

![[Illustration: Cartoon scene showing Ferris opening a floating treasure chest. Inside one chest is a glowing key labeled "Some(key)". The other chest is empty with a gentle "None" tag. A friendly compiler robot holds a checklist saying "Always check both!". Style: playful, educational, warm lighting, children's book, 16:9.]](../assets/images/6.3.png)

---

### ۶.۴. ریموت کنترل هوشمند (Match)

#### ۶.۴.۱. مشکل: چطور بر اساس مقدار enum تصمیم بگیریم؟
حالا که می‌دانیم هوا `Sunny` است یا `Rainy`، چطور به کاربر بگوییم چه لباسی بپوشد؟ می‌توانیم از چند تا `if` استفاده کنیم، اما Rust یک ابزار خیلی قشنگ‌تر دارد: `match`.

#### ۶.۴.۲. معرفی match
`match` مثل یک دستگاه جورکننده است: یک مقدار را می‌گیرد و با الگوهای مختلف مقایسه می‌کند. اولین الگویی که جواب بدهد، اجرا می‌شود.
```rust
let weather = Weather::Sunny;

match weather {
    Weather::Sunny => println!("کلاه آفتابی بگذار!"),
    Weather::Rainy => println!("چتر بردار!"),
    Weather::Snowy => println!("شال‌گردن ببند!"),
    Weather::Cloudy => println!("هوا عالی است، هر چه دوست داری!"),
}
```

#### ۶.۴.۳. شرط exhaustive (همه حالت‌ها باید پوشش داده شوند)
در `match` باید **همه‌ی** حالت‌های ممکن را بررسی کنی. اگر حتی یکی را فراموش کنی، کامپایلر بهت خطا می‌دهد و می‌گوید «فلان حالت را پوشش نداده‌ای». این خیلی خوب است چون دیگر حالت‌های فراموش‌شده باعث باگ نمی‌شوند!

#### ۶.۴.۴. استخراج داده از enum با match
اگر enum ما داده‌ی اضافی داشته باشد، می‌توانیم آن داده را در `match` بیرون بکشیم و استفاده کنیم:
```rust
let info = WeatherInfo::Sunny { temperature: 35 };

match info {
    WeatherInfo::Sunny { temperature } => {
        println!("آفتابی با دمای {} درجه، کلاه بگذار!", temperature);
    }
    WeatherInfo::Rainy { umbrella_color } => {
        println!("بارونی، چتر {} را بردار", umbrella_color);
    }
    // بقیه حالت‌ها...
}
```

#### ۶.۴.۵. الگوی catch-all با `_`
گاهی فقط به یک یا دو حالت اهمیت می‌دهیم و بقیه برایمان فرقی ندارند. می‌توانیم از `_` (خط زیرین) به معنی «هر چیز دیگر» استفاده کنیم:
```rust
match weather {
    Weather::Sunny => println!("بریم پارک!"),
    _ => println!("امروز خانه بمانیم بهتر است"),
}
```

#### ۶.۴.۶. match با Option
`match` با `Option` خیلی خوب جواب می‌دهد:
```rust
let key = Some(String::from("کلید طلایی"));

match key {
    Some(k) => println!("کلید پیدا شد: {}", k),
    None => println!("کلید گم شده، باید بگردیم!"),
}
```

#### ۶.۴.۷. if let برای ساده‌تر شدن
اگر فقط به یک حالت خاص اهمیت می‌دهیم و می‌خواهیم بقیه را نادیده بگیریم، می‌توانیم از `if let` استفاده کنیم که کوتاه‌تر است:
```rust
let weather = Weather::Sunny;

if let Weather::Sunny = weather {
    println!("امروز آفتابی و قشنگ است!");
} else {
    println!("آفتابی نیست.");
}
```

#### ۶.۴.۸. تمرین: ارزش سکه‌ها
یک enum به اسم `Coin` با حالت‌های `Penny`، `Nickel`، `Dime` و `Quarter` بساز. سپس تابعی بنویس که یک سکه بگیرد و ارزشش را به سنت برگرداند (Penny=1, Nickel=5, Dime=10, Quarter=25).

💡 **پاسخ:**
```rust
enum Coin { Penny, Nickel, Dime, Quarter }

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

![[Illustration: A cartoon remote control with four glowing buttons labeled with enum variants (Sunny, Rainy, Snowy, Cloudy). A hand presses "Rainy" and a speech bubble pops up saying "چتر بردار!". Ferris watches from the side holding a checklist. Style: dynamic, educational vector illustration, bright colors, 16:9.]](../assets/images/6.4.png)

---

### ۶.۵. پروژه: ماشین لباسشویی هوشمند
حالا با هم یک برنامه‌ی کوچک می‌نویسیم که از کاربر وضعیت آب و هوا را بپرسد و بر اساسش یک رنگ لباس پیشنهاد بدهد.

#### ۶.۵.۱. تعریف enum برای آب و هوا
```rust
enum Weather {
    Sunny,
    Rainy,
    Snowy,
    Cloudy,
}
```

#### ۶.۵.۲. تابع پیشنهاد لباس
```rust
fn recommend_shirt(weather: Weather) -> &'static str {
    match weather {
        Weather::Sunny => "سفید (خنک و آفتابی)",
        Weather::Rainy => "آبی (مثل آسمان بارونی)",
        Weather::Snowy => "قرمز (گرم و شاد)",
        Weather::Cloudy => "خاکستری (مناسب هوای ابری)",
    }
}
```
💡 `&'static str` یعنی یک رشته‌ی ثابت که همیشه در برنامه هست و نیازی به ساخت دوباره ندارد. برای متن‌های کوتاه و از پیش مشخص شده عالی است.

#### ۶.۵.۳. گرفتن ورودی از کاربر
```rust
use std::io;

fn main() {
    println!("وضعیت هوا را انتخاب کن:");
    println!("1: آفتابی | 2: بارانی | 3: برفی | 4: ابری");

    let mut input = String::new();
    io::stdin().read_line(&mut input).expect("خطا در خواندن");

    let choice: u32 = input.trim().parse().expect("لطفاً یک عدد وارد کن");

    let weather = match choice {
        1 => Weather::Sunny,
        2 => Weather::Rainy,
        3 => Weather::Snowy,
        4 => Weather::Cloudy,
        _ => {
            println!("عدد نامعتبر، پیش‌فرض آفتابی در نظر گرفته شد.");
            Weather::Sunny
        }
    };

    let shirt = recommend_shirt(weather);
    println!("پیشنهاد من: پیراهن {}", shirt);
}
```

#### ۶.۵.۴. استفاده از Option برای رنگ دلخواه
حالا فرض کن کاربر یک رنگ خاص دوست دارد. اگر وارد کرد، از همان استفاده کن، در غیر این صورت پیشنهاد خودمان را بده:
```rust
let preferred_color: Option<String> = None; // می‌توانیم بعداً از کاربر بپرسیم
let final_color = match preferred_color {
    Some(color) => color,
    None => recommend_shirt(weather).to_string(),
};
println!("رنگ نهایی: {}", final_color);
```

![[Illustration: A friendly cartoon robot washing machine/display panel showing a weather input screen. A dropdown enum selector points to a suggested shirt popping out of a slot. Ferris stands beside holding a rainbow-colored shirt. Style: cozy tech, children's book illustration, bright and inviting, 16:9.]](../assets/images/6.5.png)

---

### ۶.۶. جمع‌بندی و چالش

#### ۶.۶.۱. مرور مفاهیم
در این فصل یاد گرفتی:  
✅ `enum` نوعی است که فقط می‌تواند یکی از چند حالت مشخص را داشته باشد.  
✅ هر حالت می‌تواند داده‌ی مخصوص خودش را داشته باشد.  
✅ `Option<T>` یک enum استاندارد برای «یا چیزی هست، یا هیچی نیست» (`Some(T)` یا `None`).  
✅ `match` دستگاهی برای تصمیم‌گیری بر اساس مقدار enum و استخراج داده‌های درون آن است.  
✅ `if let` شکل خلاصه‌شده‌ی `match` برای وقتی فقط یک حالت مهم است.

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> تطبیق الگو با `match` – مخصوصاً وقتی داده از درون enum بیرون می‌کشی – ممکن است در ابتدا کمی دشوار به نظر برسد. نگران نباش! در کدهای واقعی Rust بارها و بارها از `match` استفاده می‌شود. هر بار که از آن استفاده کنی، برایت آسان‌تر خواهد شد. تمرین کن و لذت ببر!

#### ۶.۶.۲. چالش: ماشین حساب با Result
به جای `Option`، از یک enum دیگر به اسم `Result` استفاده می‌کنیم که برای مدیریت خطاها عالی است:
```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```
یک تابع `divide` بنویس که دو `f64` بگیرد و اگر مقسوم‌علیه صفر نبود، `Ok(result)` برگرداند، در غیر این صورت `Err("تقسیم بر صفر")` برگرداند. سپس در `main` با `match` نتیجه را چاپ کن.

💡 **پاسخ نمونه:**
```rust
fn divide(a: f64, b: f64) -> Result<f64, &'static str> {
    if b == 0.0 {
        Err("تقسیم بر صفر امکان‌پذیر نیست")
    } else {
        Ok(a / b)
    }
}

fn main() {
    let result = divide(10.0, 2.0);
    match result {
        Ok(r) => println!("نتیجه: {}", r),
        Err(e) => println!("خطا: {}", e),
    }
}
```
حالا تو می‌دانی چطور با `enum` و `match` حالت‌های مختلف را به زیبایی مدیریت کنی. در فصل بعد، یاد می‌گیریم چطور کدهایمان را در فایل‌ها و ماژول‌های مختلف سازماندهی کنیم تا مثل یک کتابخانه‌ی بزرگ و مرتب شود! 📚✨

![[Illustration: Ferris the crab wearing a graduation cap, holding a glowing "Chapter 6 Complete" badge. Floating around him are colorful enum tags, match arms, Option/Result boxes, and a small weather remote. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/6.6.png)
