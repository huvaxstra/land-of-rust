# 📄 فایل `README.md` (نسخه‌ی به‌روزرسانی‌شده)

در این نسخه، بخش‌های **Book Structure** و **For Rust Edu Reviewers** دقیقاً بر اساس پیشرفت پروژه (آماده‌شدن فصل‌های ۵ و ۶) و ساختار جدید ریپازیتوری اصلاح شدند. لحن، فرمت و سایر بخش‌ها حفظ شده‌اند.

```markdown
# 🦀 The Land of Rust – Ferris the Crab's Space Adventures

> A gentle, story-driven introduction to Rust programming for children (ages 9+) and absolute beginners.

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Rust Edition](https://img.shields.io/badge/rust-2021%2B-blue)](https://doc.rust-lang.org/edition-guide/)
[![Rust Version](https://img.shields.io/badge/rust-1.75%2B-blue)](https://www.rust-lang.org/)
[![Status: In Development](https://img.shields.io/badge/status-in%20development-yellow)](#)

---

## 🌟 Why Rust as a First Language?

> "Why should kids learn Rust first? Because it teaches you to think like an engineer – safely, creatively, and with a friendly crab by your side."

Most introductory programming books start with Python or Scratch. **The Land of Rust** takes a different path: we believe that Rust's emphasis on safety, clarity, and explicit reasoning can actually make it an *excellent* first language – when taught through the right metaphors, stories, and pacing.

## 📖 About This Book

**The Land of Rust** follows **Ferris**, a curious space crab whose spaceship crashes on Earth. To repair his ship and return home, Ferris must learn to communicate with an old Earth computer – and the only language it understands is Rust.

Through playful adventures, readers learn programming concepts alongside Ferris:
- 🎒 **Ownership** = A toy borrowing club with clear rules
- ⏰ **Lifetimes** = Yogurt expiration dates – nothing lasts forever!
- 🧩 **Traits** = Clay molds that shape different objects the same way
- 🔐 **Safety** = Wearing a helmet while riding your space scooter

No prior coding experience is required – just curiosity, a computer, and a willingness to explore.

## 🎯 Target Audience

| Group | Details |
|-------|---------|
| 👧 Children 9–11 | With parent/teacher guidance; focus on concepts & simple projects |
| 👦 Teens 12–14 | Can work more independently; tackle intermediate projects |
| 👨‍🏫 Educators & Parents | Non-programmers welcome – teacher's guide included |
| 🧑‍💻 Adult Beginners | Zero experience? Perfect. Start your Rust journey here. |

## ✨ Key Features

- 🎨 **Story-driven curriculum**: Every concept emerges naturally from Ferris's adventures
- ✍️ **No copy-paste culture**: Readers type every example to build muscle memory
- 🛠️ **Project-based learning**: Each chapter ends with a runnable mini-project
- 🧠 **Metaphors for hard topics**: Abstract concepts made concrete through everyday analogies
- 📚 **Comprehensive Teacher's Guide**: Session plans, troubleshooting, certificate template, FAQs
- ♿ **Accessible design**: Clear typography, RTL/LTR support, color-blind friendly examples

## 📚 Book Structure (20 Chapters + Teacher's Guide)

```
🌱 Beginner Level (Ages 9–11)
├── ✅ Ch 1: Ferris and the Lost Toolbox → Hello World, cargo, println!
├── ✅ Ch 2: The Missing Star Game → Variables, input, if/else, loops
├── ✅ Ch 3: The Space Chocolate Cake → Functions, data types, parameters
└── ✅ Ch 4: Ferris's Borrowing Club → Ownership, borrowing, slices

🌟 Intermediate Level (Ages 12–14)
├── ✅ Ch 5: Monster ID Cards → Structs, methods, associated functions
├── ✅ Ch 6: The Smart Wardrobe → Enums, Option, match, if let
├── 🔜 Ch 7–9: Modules, Collections, Errors → Phonebook, resilient calculator *(In progress)*
└── 🔜 Ch 10–11: Generics, Traits, Testing → Shape library, test suite *(In progress)*

🚀 Advanced Level (Ages 14+)
├── Ch 12–14: CLI, Iterators, Crates → minigrep, Fibonacci, pig_latin
├── Ch 15–17: Smart Pointers, Concurrency, OOP → Graph, counter, RPG battle
└── Ch 18–20: Macros, Unsafe, Networking → Command parser, repeat! macro, group chat
```

👉 Full detailed outline: [OUTLINE.md](./OUTLINE.md)

## 🚀 Getting Started (For Readers)

1. **Install Rust**: Follow the guided setup in Chapter 1 (`rustup`)
2. **Choose your path**: 
   - 📖 Read online via GitHub
   - 💻 Clone the repo and run examples locally
3. **Follow Ferris**: Type every example, solve exercises, build projects
4. **Ask for help**: Stuck? Check the Teacher's Guide or ask in Rust communities

## 👩‍🏫 For Teachers & Parents

A dedicated **Teacher's Guide** ([teacher-guide.md](./teacher-guide.md)) includes:
- 🎯 Age-appropriate pacing recommendations (3 skill levels)
- ⏱️ Sample 90-minute session structure
- 🔧 Troubleshooting common setup & conceptual hurdles
- 🎓 Printable completion certificate template
- ❓ FAQs for non-programmer adults supporting young learners

## 🔍 For Rust Edu Reviewers

If you're from the Rust Edu team reviewing this proposal:

- 📂 **Chapters 1–6 (English)**: `/en/chapter-[1-4].md/`
- 🎯 **Focus areas for feedback**:
  - Age-appropriateness of metaphors (e.g., toy tractor = ownership in Ch4, enum wardrobe = states in Ch6)
  - Pacing of ownership introduction (Ch4) to structs/enums (Ch5–6)
  - Project complexity alignment with target age groups
- 💬 **Preferred feedback channels**: GitHub Issues / Email

We're committed to adapting the structure based on your expert guidance!

## 📝 Licensing

| Content Type | License | Notes |
|--------------|---------|-------|
| Book text, illustrations descriptions, teacher guide | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) | Share & adapt with attribution |
| Code examples within chapters | [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) | Public domain – use freely |
| Rust logo / Ferris crab | Trademark of Rust Foundation | Used with respect; not covered by CC license |

## 🤝 Contributing

Feedback, corrections, translations, and teaching experiences are warmly welcomed!

- 🐛 Found a typo or unclear explanation? → [Please mail me](mailto:jgh.rust@gmail.com)
- 💡 Have a better metaphor or example? → [Please mail me](mailto:jgh.rust@gmail.com)
- 🌍 Want to translate to another language? → [Check CONTRIBUTING.md](./CONTRIBUTING.md)

Please read our [Code of Conduct](./CODE_OF_CONDUCT.md) – especially important as this content is designed for children.

## 🌐 Community & Resources

- [Rust Edu Zulip Channel](https://rust-lang.zulipchat.com/#narrow/stream/416462-t-community.2Frust-edu)
- [Rust Users Forum](https://users.rust-lang.org/)
- [The Rust Programming Language Book](https://doc.rust-lang.org/book/)
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/)

## 💌 Acknowledgments

- The Rust Foundation and Rust Edu team for inspiration and feedback
- Early testers: young learners, parents, and educators who shaped this book
- The global Rust community – your kindness makes learning Rust joyful

---

> 🦀 **Let's learn Rust – one space adventure at a time!** 🚀
