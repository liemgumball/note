---
Materials:
  - https://doc.rust-lang.org/book/ch00-00-introduction.html
---
Rust is proving to be a productive tool for collaborating among large teams of developers with varying levels of systems programming knowledge.
Low-level code is prone to various subtle bugs, which in most other languages can only be caught through extensive testing and careful code review by experienced developers. In Rust, the compiler plays a gatekeeper role by refusing to compile code with these elusive bugs, including concurrency bugs.

Developer tools:
- Cargo, the included dependency manager and build tool, makes adding, compiling, and managing dependencies painless and consistent across the Rust ecosystem.
- The `rustfmt` formatting tool ensures a consistent coding style across developers.
- The Rust Language Server `rust-analyzer` powers integrated development environment (IDE) integration for code completion and inline error messages.