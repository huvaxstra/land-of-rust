# سرزمین راست: ماجراهای فریس خرچنگ فضایی
## فصل ۱۵: راز جعبه‌های تو در تو (Smart Pointers)

### 📑 فهرست فصل
[۱۵.۱. جعبه‌ی هدیه (Box<T>)](#۱۵۱-جعبه‌ی-هدیه-boxt)  
[۱۵.۱.۱. داستان: کادوی بزرگ در جعبه‌ی کوچک](#۱۵۱۱-داستان-کادوی-بزرگ-در-جعبه‌ی-کوچک)  
[۱۵.۱.۲. Box<T> چیست؟](#۱۵۱۲-boxt-چیست)  
[۱۵.۱.۳. استفاده ساده از Box](#۱۵۱۳-استفاده-ساده-از-box)  
[۱۵.۱.۴. کاربرد: ساختارهای بازگشتی (لیست پیوندی)](#۱۵۱۴-کاربرد-ساختارهای-بازگشتی-لیست-پیوندی)  
[۱۵.۱.۵. تمرین: Box برای trait object](#۱۵۱۵-تمرین-box-برای-trait-object)  
[۱۵.۲. کتاب اشتراکی کتابخانه (Rc<T>)](#۱۵۲-کتاب-اشتراکی-کتابخانه-rct)  
[۱۵.۲.۱. داستان: کتابی که چند نفر همزمان می‌خوانند](#۱۵۲۱-داستان-کتابی-که-چند-نفر-همزمان-می‌خوانند)  
[۱۵.۲.۲. Rc<T> چیست؟](#۱۵۲۲-rct-چیست)  
[۱۵.۲.۳. ساختن Rc و clone کردن](#۱۵۲۳-ساختن-rc-و-clone-کردن)  
[۱۵.۲.۴. شمارش ارجاع‌ها](#۱۵۲۴-شمارش-ارجاع‌ها)  
[۱۵.۲.۵. محدودیت: فقط خواندنی و تک‌رشته](#۱۵۲۵-محدودیت-فقط-خواندنی-و-تک‌رشته)  
[۱۵.۲.۶. تمرین: Rc با چندین صاحب](#۱۵۲۶-تمرین-rc-با-چندین-صاحب)  
[۱۵.۲.۷. مشکل حلقه‌ی حافظه و راه حل Weak](#۱۵۲۷-مشکل-حلقه‌ی-حافظه-و-راه-حل-weak)  
[۱۵.۳. دفترچه یادداشت گروهی (RefCell<T>)](#۱۵۳-دفترچه-یادداشت-گروهی-refcellt)  
[۱۵.۳.۱. داستان: دفترچه‌ای که همه می‌توانند در آن بنویسند](#۱۵۳۱-داستان-دفترچه‌ای-که-همه-می‌توانند-در-آن-بنویسند)  
[۱۵.۳.۲. RefCell<T> چیست؟](#۱۵۳۲-refcellt-چیست)  
[۱۵.۳.۳. borrow و borrow_mut](#۱۵۳۳-borrow-و-borrow_mut)  
[۱۵.۳.۴. قانون‌شکنی در زمان اجرا](#۱۵۳۴-قانون‌شکنی-در-زمان-اجرا)  
[۱۵.۳.۵. ترکیب Rc و RefCell](#۱۵۳۵-ترکیب-rc-و-refcell)  
[۱۵.۳.۶. تمرین: Rc<RefCell<i32>>](#۱۵۳۶-تمرین-rcrefcelli32)  
[۱۵.۴. پروژه: سیستم ساده‌ی گراف](#۱۵۴-پروژه-سیستم-ساده‌ی-گراف)  
[۱۵.۴.۱. تعریف Node](#۱۵۴۱-تعریف-node)  
[۱۵.۴.۲. ساخت گراف با Rc<RefCell<Node>>](#۱۵۴۲-ساخت-گراف-با-rcrefcellnode)  
[۱۵.۴.۳. اضافه کردن یال](#۱۵۴۳-اضافه-کردن-یال)  
[۱۵.۴.۴. پیمایش ساده و هشدار حلقه](#۱۵۴۴-پیمایش-ساده-و-هشدار-حلقه)  
[۱۵.۵. جمع‌بندی و چالش](#۱۵۵-جمع‌بندی-و-چالش)  
[۱۵.۵.۱. مرور مفاهیم](#۱۵۵۱-مرور-مفاهیم)  
[۱۵.۵.۲. چالش: لیست دوطرفه با Rc<RefCell<Node>> و آشنایی با Weak](#۱۵۵۲-چالش-لیست-دوطرفه-با-rcrefcellnode-و-آشنایی-با-weak)

---

### ۱۵.۱. جعبه‌ی هدیه (Box<T>)

#### ۱۵.۱.۱. داستان: کادوی بزرگ در جعبه‌ی کوچک
فریس یک کادوی خیلی بزرگ و سنگین دارد که نمی‌تواند راحت جابه‌جایش کند. 🎁 ولی یک جعبه‌ی مقوایی کوچک و سبک پیدا می‌کند. کادو را می‌گذارد درون جعبه، و حالا فقط کافی است آن جعبه‌ی سبک را بردارد!  
در کامپیوتر هم دو جای نگهداری داریم:  
🔹 **Stack (پیشخوان میز کار):** خیلی سریع است، ولی جای آن کم است. فقط چیزهای کوچک را نگه می‌دارد.  
🔹 **Heap (انبار بزرگ):** جای زیادی دارد، ولی رفت‌وآمد در آن یکم کندتر است.  
وقتی داده‌مان بزرگ است، می‌فرستیمش به Heap و فقط یک آدرس کوچک (مثل بارکد) را روی Stack نگه می‌داریم. `Box<T>` دقیقاً همان جعبه‌ی مقوایی است که این کار را برایمان انجام می‌دهد! 📦✨

#### ۱۵.۱.۲. Box<T> چیست؟
`Box<T>` یک اشاره‌گر هوشمند است که داده‌ی نوع `T` را می‌برد در Heap ذخیره کند. وقتی `Box` از بین برود (مثلاً از تابع خارج شویم)، داده‌ی داخل Heap هم خودکار پاک می‌شود.  
سه کاربرد اصلی دارد:  
۱. ذخیره‌ی داده‌های بزرگ بدون اشغال کردن Stack.  
۲. ساخت ساختارهای بازگشتی (مثل لیست‌های زنجیره‌ای).  
۳. نگه داشتن Trait Objectها (که بعداً می‌بینیم).

#### ۱۵.۱.۳. استفاده ساده از Box
```rust
fn main() {
    let b = Box::new(5); // عدد ۵ می‌رود در Heap، آدرسش روی Stack می‌ماند
    println!("مقدار داخل جعبه: {}", b); // مثل یک عدد معمولی ازش استفاده می‌کنیم
}
```

#### ۱۵.۱.۴. کاربرد: ساختارهای بازگشتی (لیست پیوندی)
فرض کن می‌خواهیم یک قطار بسازیم که هر واگن به واگن بعدی وصل شود. در Rust نمی‌توانیم یک `struct` بنویسیم که مستقیم خودش را داخل خودش داشته باشد (چون اندازه‌اش نامحدود می‌شود!). اما با `Box` که اندازه‌اش ثابت است، مشکلی نداریم:
```rust
enum List {
    Cons(i32, Box<List>), // یک عدد + اشاره‌گر به ادامه‌ی قطار
    Nil,                  // واگن آخر (خالی)
}

use List::{Cons, Nil};

fn main() {
    let train = Cons(1, Box::new(Cons(2, Box::new(Cons(3, Box::new(Nil))))));
}
```

#### ۱۵.۱.۵. تمرین: Box برای trait object
یک Trait به اسم `Draw` با متد `draw(&self)` بساز. دو struct `Circle` و `Square` برای آن بنویس. بعد یک `Vec<Box<dyn Draw>>` بساز و شکل‌ها را در آن بریز و `draw` هر کدام را صدا بزن.

💡 **پاسخ:**
```rust
trait Draw { fn draw(&self); }

struct Circle;
impl Draw for Circle { fn draw(&self) { println!("○ دایره کشیده شد!"); } }

struct Square;
impl Draw for Square { fn draw(&self) { println!("□ مربع کشیده شد!"); } }

fn main() {
    let shapes: Vec<Box<dyn Draw>> = vec![Box::new(Circle), Box::new(Square)];
    for shape in shapes { shape.draw(); }
}
```

![[Illustration: A friendly cartoon crab (Ferris) holding a small glowing gift box labeled "Box<T>". Inside the box, a larger, heavy golden item sits safely. A conveyor belt moves the box to a large warehouse labeled "Heap", while a small barcode tag stays on a desk labeled "Stack". Style: vibrant children's book illustration, educational metaphor, soft lighting, 16:9.]](../assets/images/15.1.png)

---

### ۱۵.۲. کتاب اشتراکی کتابخانه (Rc<T>)

#### ۱۵.۲.۱. داستان: کتابی که چند نفر همزمان می‌خوانند
در کتابخانه‌ی فریس، یک کتاب خیلی معروف است. چند نفر می‌خواهند همزمان امانتش بگیرند. در Rust معمولی هر مقدار فقط یک صاحب دارد، ولی با `Rc<T>` (مخفف Reference Counted) می‌توانیم چندین صاحب همزمان داشته باشیم. `Rc` می‌شمارد چند نفر کتاب را دستشان گرفته‌اند. وقتی آخرین نفر کتاب را پس بدهد، کتاب خودکار به قفسه برمی‌گردد (حافظه پاک می‌شود). 📚🔢

#### ۱۵.۲.۲. Rc<T> چیست؟
`Rc<T>` یک اشاره‌گر هوشمند با شمارش ارجاع است. هر بار که یک `Rc` جدید از آن می‌سازی، یک شمارنده‌ی مخفی یکی اضافه می‌شود. وقتی یک `Rc` از بین برود، شمارنده کم می‌شود. به صفر که برسد، داده پاک می‌شود.  
برای استفاده باید واردش کنیم: `use std::rc::Rc;`

#### ۱۵.۲.۳. ساختن Rc و clone کردن
```rust
let a = Rc::new(5);      // شمارنده = ۱
let b = Rc::clone(&a);   // شمارنده = ۲ (دقت کن: داده کپی نمی‌شود، فقط شمارنده زیاد می‌شود)
let c = Rc::clone(&a);   // شمارنده = ۳
```

#### ۱۵.۲.۴. شمارش ارجاع‌ها
می‌توانیم تعداد قرض‌گیرنده‌ها را ببینیم:
```rust
let book = Rc::new(String::from("کتاب جادویی"));
println!("تعداد قرض‌گیرنده‌ها: {}", Rc::strong_count(&book)); // ۱
let reader = Rc::clone(&book);
println!("تعداد قرض‌گیرنده‌ها: {}", Rc::strong_count(&book)); // ۲
```

#### ۱۵.۲.۵. محدودیت: فقط خواندنی و تک‌رشته
⚠️ `Rc` فقط اجازه می‌دهد داده را **ببینی** (قرض غیرقابل تغییر). اگر بخواهی تغییرش دهی باید با `RefCell` ترکیبش کنی.  
⚠️ همچنین `Rc` فقط برای برنامه‌های تک‌رشته‌ای امن است. برای برنامه‌های چندرشته‌ای از پسرعموش `Arc` استفاده می‌کنیم.

#### ۱۵.۲.۶. تمرین: Rc با چندین صاحب
یک `struct` به اسم `Book` با فیلد `title` بساز. سه `Rc<Book>` بساز که همگی به یک کتاب اشاره کنند. عنوان را چاپ کن و تعداد ارجاع‌ها را نشان بده.

💡 **پاسخ:**
```rust
use std::rc::Rc;
struct Book { title: String }

fn main() {
    let book = Rc::new(Book { title: String::from("ماجراهای فریس") });
    let r1 = Rc::clone(&book);
    let r2 = Rc::clone(&book);
    println!("عنوان: {}", book.title);
    println!("خواننده‌ها: {}", Rc::strong_count(&book)); // ۳
}
```

#### ۱۵.۲.۷. مشکل حلقه‌ی حافظه و راه حل Weak
تا اینجا همه چیز خوب است، ولی یک تله وجود دارد! اگر با `Rc` یک **حلقه** درست کنیم (مثلاً گره A به B اشاره کند و B هم به A)، شمارنده‌ها هیچ‌وقت به صفر نمی‌رسند. این یعنی حافظه‌ی آن گره‌ها تا آخر برنامه **نشتی** می‌دهد (memory leak). 😟  
برای حل این مشکل، Rust یک اشاره‌گر هوشمند دیگر به اسم `Weak<T>` دارد. `Weak` هم مثل `Rc` است با این تفاوت که شمارنده‌ی اصلی را زیاد نمی‌کند (شمارنده‌ی ضعیف دارد). برای تبدیل `Rc` به `Weak` از `Rc::downgrade` استفاده می‌کنیم.  
در پروژه‌هایی مثل گراف‌های دوطرفه یا لیست‌های پیوندی دوطرفه، از `Weak` برای یکی از جهت‌ها استفاده می‌کنیم تا حلقه شکسته شود. نگران نباشید – در انتهای فصل در چالش به آن اشاره می‌کنیم و در فصل‌های پیشرفته‌تر بیشتر می‌بینیمش.

![[Illustration: A cartoon library desk with a single glowing book. Three children hold transparent "Rc" cards connected by dotted lines to the book. A small digital counter on the book shows "3". Ferris stands nearby holding a clipboard, smiling. Style: clean educational vector, bright colors, clear metaphor, 16:9.]](../assets/images/15.2.png)

---

### ۱۵.۳. دفترچه یادداشت گروهی (RefCell<T>)

#### ۱۵.۳.۱. داستان: دفترچه‌ای که همه می‌توانند در آن بنویسند
بچه‌های کتابخانه یک دفترچه‌ی مشترک دارند. همه می‌توانند بخوانندش، ولی وقتی کسی می‌خواهد در آن بنویسد، باید مطمئن شود هیچ‌کس دیگر همان لحظه ندارد می‌نویسد یا نمی‌خواند. در Rust این قانون معمولاً هنگام کامپایل چک می‌شود، ولی `RefCell<T>` این چک را می‌گذارد برای **زمان اجرا**. اگر کسی قانون را بشکند، برنامه با یک `panic!` مودبانه متوقف می‌شود. 📓✍️

#### ۱۵.۳.۲. RefCell<T> چیست؟
`RefCell<T>` یک اشاره‌گر هوشمند است که اجازه می‌دهد از یک داده‌ی به‌ظاهر ثابت، به‌صورت تغییرپذیر قرض بگیری، به شرطی که در زمان اجرا فقط یک نفر همزمان در حال نوشتن باشد.  
ورودش: `use std::cell::RefCell;`

#### ۱۵.۳.۳. borrow و borrow_mut
🔹 `.borrow()` → یک مرجع معمولی (`&T`) می‌دهد (فقط خواندن).  
🔹 `.borrow_mut()` → یک مرجع تغییرپذیر (`&mut T`) می‌دهد (خواندن + نوشتن).
```rust
let x = RefCell::new(5);
{
    let mut y = x.borrow_mut(); // قفل نوشتن باز شد
    *y += 10;
} // قفل بسته شد
println!("مقدار: {}", x.borrow()); // ۱۵
```

#### ۱۵.۳.۴. قانون‌شکنی در زمان اجرا
اگر همزمان دو تا `borrow_mut` بخواهی، برنامه متوقف می‌شود:
```rust
let x = RefCell::new(5);
let a = x.borrow_mut();
let b = x.borrow_mut(); // ❌ panic! دو نفر همزمان نمی‌توانند بنویسند
```
کامپایلر اینجا خطایی نمی‌گیرد، پس خودت باید حواست جمع باشد!

#### ۱۵.۳.۵. ترکیب Rc و RefCell
جادوی واقعی وقتی اتفاق می‌افتد که این دو تا را ترکیب کنیم: `Rc<RefCell<T>>`. این‌طوری چند نفر می‌توانند یک داده را ببینند و هر کدام (به نوبت) تغییرش دهند:
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::ops::AddAssign;

let shared = Rc::new(RefCell::new(0));
Rc::clone(&shared).borrow_mut().add_assign(5); // +۵
Rc::clone(&shared).borrow_mut().add_assign(3); // +۳
println!("نهایی: {}", shared.borrow()); // ۸
```

#### ۱۵.۳.۶. تمرین: Rc<RefCell<i32>>
یک عدد `10` از نوع `Rc<RefCell<i32>>` بساز. دو تابع `add_two` و `multiply_by_three` بنویس که هر کدام روی همان عدد کار کنند. در نهایت مقدار را چاپ کن.

💡 **پاسخ:**
```rust
fn add_two(num: &Rc<RefCell<i32>>) { *num.borrow_mut() += 2; }
fn multiply_by_three(num: &Rc<RefCell<i32>>) { *num.borrow_mut() *= 3; }

fn main() {
    let n = Rc::new(RefCell::new(10));
    add_two(&n);
    multiply_by_three(&n);
    println!("نتیجه: {}", n.borrow()); // ۳۶
}
```

![[Illustration: A cartoon notebook on a table with a glowing lock icon. One hand holds a blue key labeled "borrow", another hand waits with a golden key labeled "borrow_mut". A traffic light shows green for reading, red for simultaneous writing. Ferris explains with a pointer. Style: playful educational illustration, clear visual rules, bright, 16:9.]](../assets/images/15.3.png)

---

### ۱۵.۴. پروژه: سیستم ساده‌ی گراف

حالا بیا همه‌ی این جعبه‌ها را بگذاریم کنار هم و یک نقشه‌ی فضایی بسازیم! گراف مجموعه‌ای از گره‌هاست که می‌توانند به هم وصل شوند. 🌌🔗

#### ۱۵.۴.۱. تعریف Node
```rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug)]
struct Node {
    name: String,
    neighbors: Vec<Rc<RefCell<Node>>>,
}
```

#### ۱۵.۴.۲. ساخت گراف با Rc<RefCell<Node>>
```rust
fn main() {
    let a = Rc::new(RefCell::new(Node { name: "سیاره الف".into(), neighbors: vec![] }));
    let b = Rc::new(RefCell::new(Node { name: "سیاره ب".into(), neighbors: vec![] }));
    let c = Rc::new(RefCell::new(Node { name: "سیاره ج".into(), neighbors: vec![] }));

    // الف به ب و ج وصل است
    a.borrow_mut().neighbors.push(Rc::clone(&b));
    a.borrow_mut().neighbors.push(Rc::clone(&c));

    // ب هم به الف وصل است (راه دوطرفه)
    b.borrow_mut().neighbors.push(Rc::clone(&a));

    println!("همسایه‌های الف: {:?}", a.borrow().neighbors.iter().map(|n| &n.borrow().name).collect::<Vec<_>>());
}
```

#### ۱۵.۴.۳. اضافه کردن یال
می‌توانیم یک تابع کمکی بسازیم تا وصل کردن گره‌ها راحت‌تر شود:
```rust
fn add_edge(from: &Rc<RefCell<Node>>, to: &Rc<RefCell<Node>>) {
    from.borrow_mut().neighbors.push(Rc::clone(to));
}
```

#### ۱۵.۴.۴. پیمایش ساده و هشدار حلقه
⚠️ **هشدار مهم:** اگر در گراف حلقه (Cycle) باشد، پیمایش ساده ممکن است تا ابد ادامه پیدا کند! برای پیمایش امن باید یک `HashSet` از گره‌های دیده‌شده نگه داریم.  
⚠️ **نشتی حافظه:** اگر گراف دارای حلقه باشد و همه‌ی اتصالات با `Rc` باشند، حافظه‌ی آن گره‌ها هیچ‌وقت آزاد نمی‌شود (همان مشکل بخش ۱۵.۲.۷). برای ساختن گراف‌های حرفه‌ای، باید از `Weak` برای برخی یال‌ها استفاده کنیم. فعلاً نگران نباش – این فصل مقدمه‌ای بر این مفاهیم است.

![[Illustration: A star map with glowing planet nodes labeled A, B, C. Glowing lines connect them bidirectionally. Small floating boxes labeled "Rc" and "RefCell" hover near each node, showing data flow. Ferris points to a connection with a space pen. Style: cozy sci-fi workspace, educational vector, soft glow, 16:9.]](../assets/images/15.4.png)

---

### ۱۵.۵. جمع‌بندی و چالش

#### ۱۵.۵.۱. مرور مفاهیم
| ابزار | کاربرد اصلی | محدودیت مهم |
|-------|-------------|-------------|
| `Box<T>` | فرستادن داده به Heap، ساختار بازگشتی | فقط یک صاحب دارد |
| `Rc<T>` | چند صاحب همزمان (تک‌رشته) | فقط خواندنی؛ خطر نشتی در حلقه‌ها |
| `Weak<T>` | شکستن حلقه‌های `Rc` | برای دسترسی باید به `upgrade` تبدیل شود |
| `RefCell<T>` | تغییر داده از طریق مرجع ثابت | قوانین قرض‌دهی در زمان اجرا چک می‌شود |
| `Rc<RefCell<T>>` | چند صاحب + قابلیت تغییر (نوبتی) | خطر Panic در صورت نقض قانون + خطر نشتی حلقه |

#### ۱۵.۵.۲. چالش: لیست دوطرفه با Rc<RefCell<Node>> و آشنایی با Weak
یک لیست پیوندی دوطرفه بساز. هر گره فیلدهای `prev` و `next` داشته باشد. از `Option<Rc<RefCell<Node>>>` استفاده کن.  

💡 **نکته‌ی حرفه‌ای:** در دنیای واقعی، اگر از `Rc` هم برای `prev` و هم `next` استفاده کنی، یک حلقه‌ی حافظه (Memory Leak) درست می‌شود. راه حل استاندارد این است که برای `prev` از `Weak<RefCell<Node>>` استفاده کنی. شکل نهایی چنین چیزی خواهد بود:

```rust
use std::rc::{Rc, Weak};
use std::cell::RefCell;

struct Node {
    value: i32,
    next: Option<Rc<RefCell<Node>>>,
    prev: Option<Weak<RefCell<Node>>>,
}
```

فعلاً اگر فقط با `Rc` تمرین کنی، اشکالی ندارد – ولی بدان که برای کدنویسی واقعی باید از `Weak` استفاده کرد. اگر خواستی می‌توانی همین حالا `Weak` را جایگزین کنی و با `upgrade` به آن دسترسی پیدا کنی. 🧠

![[Illustration: Ferris wearing a graduation cap and safety goggles, holding a glowing "Chapter 15 Master" badge. Floating around him are a gift box (Box), a shared book (Rc), a notebook with a lock (RefCell), and a small star map graph. Encouraging, bright lighting, children's book style, 16:9.]](../assets/images/15.5.png)
