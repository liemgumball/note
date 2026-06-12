

> [!NOTE] 
> This is similar to Ruby’s [rbenv](https://github.com/rbenv/rbenv), Python’s [pyenv](https://github.com/yyuu/pyenv), or Node’s [nvm](https://github.com/creationix/nvm).

# Terminology
- **channel** - Rust is released in three channels: *stable*, *beta*, *nightly*
- **toolchain** - A “toolchain” is a complete installation of the Rust compiler (`rustc`) and related tools (like `cargo`). A [toolchain specification](https://rust-lang.github.io/rustup/concepts/toolchains.html) includes the release channel or version, and the host platform that the toolchain runs on.
- **component** — Each release of Rust includes several “components”, some of which are required (like `rustc`) and some that are optional (like [`clippy`](https://github.com/rust-lang/rust-clippy)).
- **proxy** — A wrapper for a common Rust component (like `rustc`), built to forward CLI invocations to the active Rust toolchain.
- **profile** — Defines a grouping of components.