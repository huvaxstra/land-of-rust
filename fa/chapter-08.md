# سرزمین راست: ماجراهای فریس خرچنگ فضایی  
## فصل ۸: جعبه‌های جادویی که بزرگ و کوچک می‌شوند (Collections)

### 📑 فهرست فصل
[۸.۱. لیست خرید مامان (Vector)](#۸۱-لیست-خرید-مامان-vector)  
[۸.۱.۱. داستان: لیست خرید فریس](#۸۱۱-داستان-لیست-خرید-فریس)  
[۸.۱.۲. معرفی Vec<T>](#۸۱۲-معرفی-vec)  
[۸.۱.۳. ساختن وکتور](#۸۱۳-ساختن-وکتور)  
[۸.۱.۴. اضافه کردن عنصر با push](#۸۱۴-اضافه-کردن-عنصر-با-push)  
[۸.۱.۵. حذف آخرین عنصر با pop](#۸۱۵-حذف-آخرین-عنصر-با-pop)  
[۸.۱.۶. دسترسی به عناصر (اندیس و get)](#۸۱۶-دسترسی-به-عناصر-اندیس-و-get)  
[۸.۱.۷. حلقه زدن روی وکتور](#۸۱۷-حلقه-زدن-روی-وکتور)  
[۸.۱.۸. تمرین: جمع و میانگین](#۸۱۸-تمرین-جمع-و-میانگین)  
[۸.۲. دفترچه تلفن مخفی (HashMap)](#۸۲-دفترچه-تلفن-مخفی-hashmap)  
[۸.۲.۱. داستان: دفترچه تلفن فریس](#۸۲۱-داستان-دفترچه-تلفن-فریس)  
[۸.۲.۲. معرفی HashMap<K, V>](#۸۲۲-معرفی-hashmap)  
[۸.۲.۳. ساختن HashMap](#۸۲۳-ساختن-hashmap)  
[۸.۲.۴. درج و به‌روزرسانی (insert)](#۸۲۴-درج-و-به‌روزرسانی-insert)  
[۸.۲.۵. دریافت مقدار (get)](#۸۲۵-دریافت-مقدار-get)  
[۸.۲.۶. بررسی وجود کلید (contains_key)](#۸۲۶-بررسی-وجود-کلید-contains_key)  
[۸.۲.۷. حذف با remove](#۸۲۷-حذف-با-remove)  
[۸.۲.۸. به‌روزرسانی شرطی با entry و or_insert](#۸۲۸-به‌روزرسانی-شرطی-با-entry-و-or_insert)  
[۸.۲.۹. حلقه زدن روی HashMap](#۸۲۹-حلقه-زدن-روی-hashmap)  
[۸.۲.۱۰. تمرین: شمارش کلمات](#۸۲۱۰-تمرین-شمارش-کلمات)  
[۸.۳. داستانک: گردآوری آیتم‌های یک بازی نقش‌آفرینی](#۸۳-داستانک-گردآوری-آیتم‌های-یک-بازی-نقش‌آفرینی)  
[۸.۳.۱. تعریف struct Item](#۸۳۱-تعریف-struct-item)  
[۸.۳.۲. کیسه‌ی آیتم‌ها (Vec)](#۸۳۲-کیسهی-آیتم‌ها-vec)  
[۸.۳.۳. نقشه‌ی گنج (HashMap)](#۸۳۳-نقشهی-گنج-hashmap)  
[۸.۳.۴. توابع کمکی](#۸۳۴-توابع-کمکی)  
[۸.۳.۵. داستان تعاملی](#۸۳۵-داستان-تعاملی)  
[۸.۴. عملکرد و انتخاب درست](#۸۴-عملکرد-و-انتخاب-درست)  
[۸.۴.۱. چه زمانی از وکتور استفاده کنیم؟](#۸۴۱-چه-زمانی-از-وکتور-استفاده-کنیم)  
[۸.۴.۲. چه زمانی از هش‌مپ استفاده کنیم؟](#۸۴۲-چه-زمانی-از-هش‌مپ-استفاده-کنیم)  
[۸.۴.۳. معرفی HashSet (بدون مقدار)](#۸۴۳-معرفی-hashset-بدون-مقدار)  
[۸.۴.۴. تمرین: اشتراک دو لیست](#۸۴۴-تمرین-اشتراک-دو-لیست)  
[۸.۵. پروژه: دفترچه تلفن تعاملی](#۸۵-پروژه-دفترچه-تلفن-تعاملی)  
[۸.۵.۱. منوی اصلی](#۸۵۱-منوی-اصلی)  
[۸.۵.۲. اضافه کردن مخاطب](#۸۵۲-اضافه-کردن-مخاطب)  
[۸.۵.۳. جستجوی مخاطب](#۸۵۳-جستجوی-مخاطب)  
[۸.۵.۴. حذف مخاطب](#۸۵۴-حذف-مخاطب)  
[۸.۵.۵. نمایش همه](#۸۵۵-نمایش-همه)  
[۸.۶. جمع‌بندی و چالش](#۸۶-جمع‌بندی-و-چالش)  
[۸.۶.۱. مرور مفاهیم](#۸۶۱-مرور-مفاهیم)  
[۸.۶.۲. چالش: سیستم نمرات دانش‌آموزان](#۸۶۲-چالش-سیستم-نمرات-دانش‌آموزان)  

---

### ۸.۱. لیست خرید مامان (Vector)

#### ۸.۱.۱. داستان: لیست خرید فریس
مامان فریس قبل از رفتن به فروشگاه، همیشه یک تکه کاغذ برمی‌دارد و چیزهایی که لازم دارند را می‌نویسد: «شیر، نان، تخم‌مرغ، سیب». 🛒 وقتی در فروشگاه می‌چرخند، ممکن است یکهو یادش بیاید: «آها! پنیر هم لازم داریم!» و سریع آن را به ته لیست اضافه می‌کند. وقتی هم چیزی را برمی‌دارد، خط می‌زندش.

در برنامه‌نویسی هم دقیقاً به همین لیست‌های هوشمند نیاز داریم که بتوانند بزرگ و کوچک شوند. یادت می‌آید در فصل ۳ آرایه (`[]`) را یاد گرفتیم؟ آرایه‌ها اندازه‌شان ثابت است و نمی‌شود بعداً چیزی بهشان اضافه کرد. اما **وکتور (Vector)** دقیقاً همان لیست خرید جادویی ماست!  
**مدیریت داده‌های در حال تغییر یکی از مهارت‌های اصلی هر برنامه‌نویس حرفه‌ای است. این یعنی گامی دیگر به سوی جادوگر کامپیوتر شدن!** 🧙‍♂️

> 👨‍👩‍👧 **نکته برای والدین و مربیان**  
> وکتورها و هش‌مپ‌ها از ساختارهای داده‌ی بنیادین در تمام زبان‌های برنامه‌نویسی هستند. این فصل نشان می‌دهد چطور داده‌ها را ذخیره، دسترسی و به‌روزرسانی کنیم – مهارتی که در نرم‌افزارهای واقعی مدام استفاده می‌شود. کتاب رسمی Rust فصل کاملی درباره‌ی مجموعه‌ها دارد:  
> [doc.rust-lang.org/book/ch08-00-common-collections.html](https://doc.rust-lang.org/book/ch08-00-common-collections.html)

![[Illustration: A cute cartoon crab (Ferris) holding a magical floating shopping list that keeps growing and shrinking. Items like milk, bread, eggs, and cheese pop in and out with sparkles. Background: a cozy space-market aisle with glowing shelves. Style: vibrant children's book illustration, playful, high quality, 16:9.]](../assets/images/8.1.png)

#### ۸.۱.۲. معرفی `Vec<T>`
`Vec<T>` یک جعبه‌ی هوشمند است که می‌تواند تعداد زیادی از یک نوع (`T`) را پشت سر هم نگه دارد. آن `T` می‌تواند هر چیزی باشد: عدد، متن، یا حتی `struct`هایی که خودمان ساختیم. بهترین ویژگی وکتور این است که اندازه‌اش ثابت نیست و هر وقت بخواهی می‌توانی بهش اضافه کنی یا ازش کم کنی.

#### ۸.۱.۳. ساختن وکتور
دو راه اصلی برای ساختن وکتور داریم:
```rust
// راه اول: ساختن یک وکتور خالی (باید نوعش را مشخص کنیم)
let mut shopping_list: Vec<String> = Vec::new();

// راه دوم: ساختن وکتور با مقدارهای اولیه (سریع و راحت با ماکروی vec!)
let mut shopping_list = vec![
    "شیر".to_string(),
    "نان".to_string()
];
```
ماکروی `vec!` خیلی کار راه‌انداز است. فقط کافی است مقادیر را با کاما جدا کنی و بین `[]` بگذاری.

#### ۸.۱.۴. اضافه کردن عنصر با `push`
برای اضافه کردن یک چیز جدید به ته وکتور، از متد `push` استفاده می‌کنیم:
```rust
shopping_list.push("تخم‌مرغ".to_string());
shopping_list.push("سیب".to_string());
```
حالا وکتور ما چهار عضو دارد: شیر، نان، تخم‌مرغ، سیب. 🥚🍎

#### ۸.۱.۵. حذف آخرین عنصر با `pop`
اگر پشیمان شویم و نخواهیم سیب را بخریم، می‌توانیم با `pop` آخرین عضو را از وکتور دربیاوریم. یک نکته‌ی مهم: `pop` یک `Option<T>` برمی‌گرداند! یعنی اگر وکتور خالی نباشد، `Some(آخرین_عضو)` را می‌دهد، و اگر خالی باشد `None`. این‌طوری برنامه هیچ‌وقت کرش نمی‌کند.
```rust
let last_item = shopping_list.pop();
match last_item {
    Some(item) => println!("آخرین چیزی که حذف شد: {}", item),
    None => println!("لیست از قبل خالی بود!"),
}
```

#### ۸.۱.۶. دسترسی به عناصر (اندیس و `get`)
برای خواندن یک عضو خاص با شماره (اندیس که از صفر شروع می‌شود)، دو راه داریم:

🔹 **راه سریع اما خطرناک `[]`:**
```rust
let second = &shopping_list[1]; // "نان"
// let bad = &shopping_list[10]; // ❌ اگر اندیس وجود نداشته باشد، برنامه می‌ترکد!
```

🔹 **راه امن و پیشنهادی `get`:** این روش یک `Option<&T>` برمی‌گرداند. اگر اندیس وجود داشته باشد `Some` می‌دهد، وگرنه `None`.
```rust
match shopping_list.get(1) {
    Some(item) => println!("آیتم دوم: {}", item),
    None => println!("این اندیس وجود ندارد!"),
}
```
💡 **نکته‌ی ایمنی:** همیشه تا جایی که می‌شود از `get` استفاده کن، مخصوصاً وقتی مطمئن نیستی اندیس حتماً وجود دارد.

#### ۸.۱.۷. حلقه زدن روی وکتور
برای دیدن تک‌تک اعضای وکتور، از حلقه‌ی `for` استفاده می‌کنیم:
```rust
// فقط خواندن (مرجع غیرقابل تغییر)
for item in &shopping_list {
    println!("- {}", item);
}

// اگر بخواهی اعضای وکتور را تغییر دهی، باید از &mut استفاده کنی
for item in &mut shopping_list {
    item.push_str("!"); // به ته همه‌ی آیتم‌ها یک علامت تعجب اضافه می‌کند
}
```

#### ۸.۱.۸. تمرین: جمع و میانگین
یک وکتور از اعداد صحیح (`i32`) بساز و مجموع و میانگینشان را حساب کن.

💡 **پاسخ:**
```rust
fn main() {
    let numbers = vec![10, 20, 30, 40, 50];
    
    // روش حرفه‌ای و سریع
    let sum: i32 = numbers.iter().sum();
    let count = numbers.len();
    let average = sum as f64 / count as f64;
    
    println!("مجموع: {}", sum);
    println!("میانگین: {:.2}", average); // دو رقم اعشار
}
```

![[Illustration: A cartoon vector visualized as a train of glowing train cars. Each car holds a different item (Milk, Bread, Eggs, Apple). A crab is pushing a new car "Cheese" onto the end, and another crab is popping off the last car. Style: playful, educational, bright colors, 16:9.]](../assets/images/8.2.png)

---

### ۸.۲. دفترچه تلفن مخفی (HashMap)

#### ۸.۲.۱. داستان: دفترچه تلفن فریس
فریس در کهکشان دوستان زیادی دارد: بیلی، لونا، استلا... 🌌 او یک دفترچه‌ی جادویی دارد که هر وقت اسم یک دوست را باز کند، شماره‌ی تلفن فضایی‌اش ظاهر می‌شود. در این دفترچه، هر **اسم** به یک **شماره** وصل است. در برنامه‌نویسی به این ساختار می‌گوییم **نگاشت (Map)**. در Rust اسمش `HashMap` است.

![[Illustration: A cartoon crab holding a glowing magical address book. When a page labeled "Luna" opens, a holographic phone number floats out. The background shows a starry galaxy with tiny planets. Style: whimsical, educational children's book illustration, bright colors, 16:9.]](../assets/images/8.3.png)

#### ۸.۲.۲. معرفی `HashMap<K, V>`
`HashMap<K, V>` یک جعبه‌ی هوشمند است که یک **کلید (Key)** از نوع `K` را به یک **مقدار (Value)** از نوع `V` وصل می‌کند. مزیتش این است که پیدا کردن مقدار با داشتن کلید، خیلی سریع است (حتی اگر میلیون‌ها اسم داشته باشیم).  
قبل از استفاده باید آن را از کتابخانه‌ی استاندارد وارد کنیم:
```rust
use std::collections::HashMap;
```

#### ۸.۲.۳. ساختن HashMap
```rust
let mut phone_book = HashMap::new();
```
می‌توانیم یک هش‌مپ را با مقدارهای اولیه هم بسازیم (با استفاده از `vec` و `collect`):
```rust
let data = vec![("فریس", "۱۲۳۴۵"), ("بیل", "۶۷۸۹۰")];
let phone_book: HashMap<_, _> = data.into_iter().collect();
```

#### ۸.۲.۴. درج و به‌روزرسانی (`insert`)
با متد `insert` یک جفت کلید-مقدار اضافه می‌کنیم. اگر کلید از قبل وجود داشته باشد، مقدار قبلی با مقدار جدید جایگزین می‌شود:
```rust
phone_book.insert(String::from("فریس"), String::from("۱۲۳۴۵۶"));
phone_book.insert(String::from("بیل"), String::from("۷۸۹۱۰۱"));
```

#### ۸.۲.۵. دریافت مقدار (`get`)
برای گرفتن شماره‌ی یک شخص، از `get` استفاده می‌کنیم که یک `Option<&V>` برمی‌گرداند (چون ممکن است آن شخص در دفترچه نباشد):
```rust
let name = "فریس";
match phone_book.get(name) {
    Some(number) => println!("شماره {}: {}", name, number),
    None => println!("{} در دفترچه نیست!", name),
}
```

#### ۸.۲.۶. بررسی وجود کلید (`contains_key`)
اگر فقط می‌خواهی بدانی کلیدی وجود دارد یا نه، نیازی به خواندن مقدارش نیست:
```rust
if phone_book.contains_key("فریس") {
    println!("فریس در دفترچه هست. ✅");
}
```

#### ۸.۲.۷. حذف با `remove`
با `remove` یک کلید و مقدارش را پاک می‌کنیم. خروجی‌اش `Option<V>` است (یعنی اگر پاک شد، مقدار پاک‌شده را برمی‌گرداند):
```rust
let removed = phone_book.remove("بیل");
if removed.is_some() {
    println!("بیل از دفترچه حذف شد. 🗑️");
}
```

#### ۸.۲.۸. به‌روزرسانی شرطی با `entry` و `or_insert`
گاهی می‌خواهیم بگوییم: «اگر کلید وجود نداشت، یک مقدار پیش‌فرض بگذار، اگر بود، همان را نگه دار». برای این کار از `entry` و `or_insert` استفاده می‌کنیم که خیلی برای **شمارش** کاربرد دارد:
```rust
// اگر "استلا" نبود، "۰۰۰۰" را وارد کن و یک کلید موقت به آن بده
let count = phone_book.entry("استلا").or_insert(String::from("۰۰۰۰"));
// حالا count یک &mut String است که می‌توانی تغییرش دهی
```

#### ۸.۲.۹. حلقه زدن روی HashMap
```rust
for (key, value) in &phone_book {
    println!("{} -> {}", key, value);
}
```
📌 **نکته:** ترتیب چاپ شدن در `HashMap` تضمین شده نیست! مثل یک کیسه‌ی جادویی است که هر بار دست می‌کنی، ممکن است یک چیز دیگر بیاید بیرون. ولی نگران نباش، پیدا کردنشان همیشه سریع است.

#### ۸.۲.۱۰. تمرین: شمارش کلمات
برنامه‌ای بنویس که یک جمله را از کاربر بگیرد و تعداد تکرار هر کلمه را در یک `HashMap` بشمارد.

💡 **پاسخ:**
```rust
use std::collections::HashMap;
use std::io;

fn main() {
    println!("یک جمله بنویس:");
    let mut text = String::new();
    io::stdin().read_line(&mut text).expect("خطا");

    let mut counts = HashMap::new();

    // جمله را بر اساس فاصله تکه‌تکه می‌کنیم
    for word in text.split_whitespace() {
        let count = counts.entry(word).or_insert(0);
        *count += 1; // علامت * یعنی محتوای مرجع را تغییر بده (چون count یک &mut i32 است)
    }

    println!("\nتعداد تکرار کلمات:");
    for (word, count) in &counts {
        println!("{}: {}", word, count);
    }
}
```

![[Illustration: A cartoon address book with pages that have key-value pairs (Ferris→12345, Bill→67890, Luna→99999). A magical magnifying glass highlights the "Luna" page, and a holographic number pops out. Style: educational, whimsical, bright colors, 16:9.]](../assets/images/8.4.png)

---

### ۸.۳. داستانک: گردآوری آیتم‌های یک بازی نقش‌آفرینی

بیا با هم یک ماجراجویی کوچک بسازیم! فریس در یک سیاره‌ی ناشناخته می‌گردد و آیتم جمع می‌کند. 🗺️💎

#### ۸.۳.۱. تعریف `struct Item`
```rust
#[derive(Debug)] // این خط اجازه می‌دهد آیتم‌ها را راحت چاپ کنیم
struct Item {
    name: String,
    value: u32, // ارزش آیتم به سکه
}
```

#### ۸.۳.۲. کیسه‌ی آیتم‌ها (`Vec<Item>`)
```rust
let mut inventory: Vec<Item> = Vec::new();
inventory.push(Item { name: String::from("شمشیر چوبی"), value: 10 });
inventory.push(Item { name: String::from("معجون سلامتی"), value: 25 });
```

#### ۸.۳.۳. نقشه‌ی گنج (`HashMap<String, u32>`)
یک نقشه از مکان‌های مختلف و مقدار گنجی که در آنها پنهان شده:
```rust
let mut treasure_map = HashMap::new();
treasure_map.insert(String::from("غار تاریک"), 500);
treasure_map.insert(String::from("جنگل مه‌آلود"), 200);
treasure_map.insert(String::from("قله برفی"), 1000);
```

#### ۸.۳.۴. توابع کمکی
```rust
fn add_item(inventory: &mut Vec<Item>, item: Item) {
    println!("✅ آیتم '{}' به کیسه اضافه شد.", item.name);
    inventory.push(item);
}

fn show_inventory(inventory: &Vec<Item>) {
    if inventory.is_empty() {
        println!("کیسه خالی است! 😢");
    } else {
        println!("🎒 کیسه تو:");
        for item in inventory {
            println!("  - {} (ارزش: {} سکه)", item.name, item.value);
        }
    }
}

fn search_treasure(map: &HashMap<String, u32>, place: &str) -> Option<u32> {
    map.get(place).copied() // .copied() مقدار &u32 را به u32 تبدیل می‌کند (کپی می‌کند)
}
```

#### ۸.۳.۵. داستان تعاملی
```rust
fn main() {
    let mut inventory = Vec::new();
    let mut treasure_map = HashMap::new();
    treasure_map.insert(String::from("غار"), 500);
    treasure_map.insert(String::from("جنگل"), 200);

    add_item(&mut inventory, Item { name: String::from("کلید زنگ‌زده"), value: 5 });
    add_item(&mut inventory, Item { name: String::from("نقشه قدیمی"), value: 50 });
    
    show_inventory(&inventory);

    let place = "غار";
    match search_treasure(&treasure_map, place) {
        Some(gold) => println!("🎉 هورا! در {} {} سکه پیدا کردی!", place, gold),
        None => println!("❌ در {} گنجی پیدا نکردی.", place),
    }
}
```

![[Illustration: A cartoon RPG game scene. Ferris stands in front of a treasure chest with a map in hand. A vector backpack is on his back with item slots (Wooden Sword, Health Potion). A glowing map table shows locations: Dark Cave, Misty Forest, Snowy Peak. Style: fantasy children's book illustration, adventurous, bright, 16:9.]](../assets/images/8.5.png)

---

### ۸.۴. عملکرد و انتخاب درست

#### ۸.۴.۱. چه زمانی از وکتور استفاده کنیم؟
✅ وقتی ترتیب اعضا مهم است (مثلاً لیست نوبت یا صف).  
✅ وقتی می‌خواهیم با اندیس (شماره) به اعضا دسترسی داشته باشیم.  
✅ وقتی بیشتر کارمان اضافه کردن به انتها یا حذف از انتها است.

#### ۸.۴.۲. چه زمانی از هش‌مپ استفاده کنیم؟
✅ وقتی می‌خواهیم با یک کلید (مثل اسم یا کد) چیزی را سریع پیدا کنیم.  
✅ وقتی ترتیب اعضا برایمان مهم نیست.  
✅ وقتی هر کلید فقط یک مقدار دارد (مثلاً شماره تلفن یک شخص).

#### ۸.۴.۳. معرفی `HashSet` (بدون مقدار)
گاهی فقط می‌خواهیم یک مجموعه از چیزهای **یکتا** داشته باشیم (مثل اسم کسانی که در مهمانی هستند). `HashSet<T>` دقیقاً مثل `HashMap` است، فقط **بدون مقدار**! خودش حواسش است که چیز تکراری اضافه نشود.
```rust
use std::collections::HashSet;

let mut names = HashSet::new();
names.insert("فریس");
names.insert("بیل");
names.insert("فریس"); // تکراری است، اضافه نمی‌شود!

println!("تعداد افراد: {}", names.len()); // ۲
```

#### ۸.۴.۴. تمرین: اشتراک دو لیست
دو وکتور از اعداد داری: `[1, 2, 3, 4, 5]` و `[4, 5, 6, 7, 8]`. اعداد مشترک را با کمک `HashSet` پیدا کن.

💡 **پاسخ:**
```rust
use std::collections::HashSet;

fn main() {
    let a = vec![1, 2, 3, 4, 5];
    let b = vec![4, 5, 6, 7, 8];

    let set_a: HashSet<_> = a.into_iter().collect();
    let set_b: HashSet<_> = b.into_iter().collect();

    let common: Vec<_> = set_a.intersection(&set_b).collect();
    println!("اعداد مشترک: {:?}", common); // [4, 5]
}
```

![[Illustration: Two overlapping magical circles labeled "List A" and "List B". In the intersection, glowing numbers "4" and "5" float with sparkles. Ferris the crab stands nearby holding a magnifying glass. Style: educational vector illustration, clean, bright, 16:9.]](../assets/images/8.6.png)

---

### ۸.۵. پروژه: دفترچه تلفن تعاملی

بیا همه‌ی چیزهایی که یاد گرفتیم را در یک پروژه‌ی کامل به کار ببریم: یک دفترچه تلفن که در ترمینال کار می‌کند. 📞

#### ۸.۵.۱. منوی اصلی
```rust
use std::collections::HashMap;
use std::io;

fn main() {
    let mut phone_book: HashMap<String, String> = HashMap::new();

    loop {
        println!("\n📞 دفترچه تلفن فریس 📞");
        println!("1. اضافه کردن مخاطب جدید");
        println!("2. جستجوی شماره");
        println!("3. حذف مخاطب");
        println!("4. نمایش همه مخاطبین");
        println!("5. خروج");

        let mut choice = String::new();
        io::stdin().read_line(&mut choice).unwrap();

        match choice.trim() {
            "1" => add_contact(&mut phone_book),
            "2" => search_contact(&phone_book),
            "3" => delete_contact(&mut phone_book),
            "4" => show_all(&phone_book),
            "5" => {
                println!("خداحافظ! 👋");
                break;
            }
            _ => println!("عدد اشتباه! دوباره انتخاب کن."),
        }
    }
}
```

#### ۸.۵.۲. اضافه کردن مخاطب
```rust
fn add_contact(book: &mut HashMap<String, String>) {
    println!("اسم مخاطب را وارد کن:");
    let mut name = String::new();
    io::stdin().read_line(&mut name).unwrap();
    let name = name.trim().to_string();

    println!("شماره تلفن را وارد کن:");
    let mut number = String::new();
    io::stdin().read_line(&mut number).unwrap();
    let number = number.trim().to_string();

    book.insert(name, number);
    println!("✅ مخاطب اضافه شد.");
}
```

#### ۸.۵.۳. جستجوی مخاطب
```rust
fn search_contact(book: &HashMap<String, String>) {
    println!("اسم مورد نظر برای جستجو:");
    let mut name = String::new();
    io::stdin().read_line(&mut name).unwrap();
    let name = name.trim();

    match book.get(name) {
        Some(number) => println!("📞 {}: {}", name, number),
        None => println!("❌ {} در دفترچه نیست.", name),
    }
}
```

#### ۸.۵.۴. حذف مخاطب
```rust
fn delete_contact(book: &mut HashMap<String, String>) {
    println!("اسم مخاطبی که می‌خواهی حذف کنی:");
    let mut name = String::new();
    io::stdin().read_line(&mut name).unwrap();
    let name = name.trim();

    if book.remove(name).is_some() {
        println!("✅ {} حذف شد.", name);
    } else {
        println!("❌ {} وجود ندارد.", name);
    }
}
```

#### ۸.۵.۵. نمایش همه
```rust
fn show_all(book: &HashMap<String, String>) {
    if book.is_empty() {
        println!("📭 دفترچه خالی است.");
    } else {
        println!("📋 لیست مخاطبین:");
        for (name, number) in book {
            println!("  {} : {}", name, number);
        }
    }
}
```

![[Illustration: A cartoon smartphone screen showing Ferris's Phonebook app interface. The screen displays menu options (Add, Search, Delete, Show All) and a sample contact list. Ferris sits next to the phone holding a pen and notebook. Style: clean, educational, bright UI metaphor, 16:9.]](../assets/images/8.7.png)

---

### ۸.۶. جمع‌بندی و چالش

#### ۸.۶.۱. مرور مفاهیم
در این فصل یاد گرفتی:
✅ `Vec<T>`: لیست قابل تغییر اندازه. (`push`, `pop`, `get`, `[]`, حلقه‌ی `for`)  
✅ `HashMap<K, V>`: نگاشت کلید به مقدار. (`insert`, `get`, `entry().or_insert()`, `remove`)  
✅ `HashSet<T>`: مجموعه‌ی بدون عضو تکراری.  
✅ تفاوت دسترسی امن (`get`) و دسترسی سریع (`[]`).  
✅ **مدیریت داده‌های پویا یعنی قدرت مدل کردن دنیای واقعی در کامپیوتر – یک جادوگر واقعی چنین می‌کند.** 🧙

> 🧠 **گاهی بعضی چیزها سخت است، و این اشکالی ندارد!**  
> انتخاب بین وکتور و هش‌مپ ممکن است در ابتدا مانند یک پازل به نظر برسد. حتی توسعه‌دهندگان حرفه‌ای گاهی برای تصمیم‌گیری به مستندات نگاه می‌کنند. با تمرین، این انتخاب برایت طبیعی می‌شود. فقط به یاد داشته باش: اگر به ترتیب نیاز داری → وکتور؛ اگر به کلید نیاز داری → هش‌مپ.

#### ۸.۶.۲. چالش: سیستم نمرات دانش‌آموزان
یک برنامه بنویس که از کاربر اسم دانش‌آموز و نمره‌اش را بگیرد. می‌تواند چند نمره برای یک دانش‌آموز وارد کند. در انتها، برای هر دانش‌آموز میانگین نمراتش را چاپ کند.  
💡 **راهنمایی:** از `HashMap<String, Vec<f64>>` استفاده کن. وقتی اسم جدید وارد می‌شود، با `entry` و `or_insert_with(Vec::new)` یک وکتور خالی برایش بساز و نمره را `push` کن.

💡 **پاسخ نمونه:**
```rust
use std::collections::HashMap;
use std::io;

fn main() {
    let mut grades: HashMap<String, Vec<f64>> = HashMap::new();

    loop {
        println!("اسم دانش‌آموز (یا 'خروج' برای پایان):");
        let mut name = String::new();
        io::stdin().read_line(&mut name).unwrap();
        let name = name.trim().to_string();
        
        if name == "خروج" { break; }

        println!("نمره:");
        let mut grade_str = String::new();
        io::stdin().read_line(&mut grade_str).unwrap();
        let grade: f64 = grade_str.trim().parse().expect("عدد وارد کن");

        grades.entry(name).or_insert_with(Vec::new).push(grade);
    }

    println!("\n📊 --- میانگین نمرات ---");
    for (name, scores) in &grades {
        let sum: f64 = scores.iter().sum();
        let avg = sum / scores.len() as f64;
        println!("{}: {:.2}", name, avg);
    }
}
```

حالا تو می‌دانی چطور از وکتورها و هش‌مپ‌ها برای ذخیره‌ی اطلاعات متغیر استفاده کنی. 🎒📦  
در فصل بعد، با **مدیریت خطا** آشنا می‌شویم و یاد می‌گیریم چطور از ترکیدن برنامه جلوگیری کنیم و خطاها را مثل یک قهرمان مدیریت کنیم! 🛡️🦀

![[Illustration: Ferris wearing a graduation cap, holding a glowing "Chapter 8 Master" badge. Floating around him are colorful Vectors, HashMaps, and Set symbols turning into a neat digital backpack. Style: encouraging, vibrant children's book illustration, 16:9.]](../assets/images/8.8.png)