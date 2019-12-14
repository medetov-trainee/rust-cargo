# rust-hello-cargo
An introduction to Cargo. This is the [`Hello, Cargo!`][1] example from [The Rust Programming Language][2] book.

### What is Cargo?
Rusts build system _and_ package manager.
- Builds your code
- Downloads the dependencies of your code
- Builds those dependencies
- Installed with Rust through main channels
- Ensures a repeatable build

Cargo does 4 things:
- Introduces two metadata files with various bits of package information.
- Fetches and builds your package’s dependencies.
- Invokes rustc or another build tool with the correct parameters to build your package.
- Introduces conventions to make working with Rust packages easier.

### [`cargo new`][3]

> This command will create a new Cargo package in the given directory. This includes a simple template with a Cargo.toml manifest, sample source file, and a VCS ignore file. If the directory is not already in a VCS repository, then a new repository is created...

```
> cargo new hello_cargo
```
`cargo new hello_cargo` creates a new project called, "hello_cargo" and Cargo creates its files in a directory of the same name. This is the contents of `.\hello_cargo`:
```
C:.
│   .gitignore
│   Cargo.toml
│
└───src
        main.rs
```

### [`Cargo.toml`][4]
> The Cargo.toml file for each package is called its manifest. Every manifest file consists of one or more sections.

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Peter <peter@rustacean.com>"]
edition = "2018"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

#### [`[package]`][5]
- Indicates section of statements necessary for program compilation.
- Name and email are sourced from environment, so edit if necessary.

#### [`[dependencies]`][6]
- Section to list project dependencies.
- In Rust, packages are referred to as Crates.
- This example has no dependencies.

### .\src directory
- Cargo expects source files to live inside `.\src` directory.
- Top level of a project directory is for README, LICENSE and other non-code related files.
- Everything has its place!

### [`cargo build`][7]
> Compile local packages and all of their dependencies.
```
PS C:\Users\peter\Documents\rust-projects\hello_cargo> cargo build
   Compiling hello_cargo v0.1.0 (C:\Users\peter\Documents\rust-projects\hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 3.67s
```
Directory structure after build:
```
C:.
│   .gitignore
│   Cargo.lock
│   Cargo.toml
│
├───src
│       main.rs
│
└───target
    │   .rustc_info.json
    │
    └───debug
        │   .cargo-lock
        │   hello_cargo.d
        │   hello_cargo.exe
        │   hello_cargo.pdb
        │
        ├───.fingerprint
        │   └───hello_cargo-a395dae34745bcde
        │           bin-hello_cargo-a395dae34745bcde
        │           bin-hello_cargo-a395dae34745bcde.json
        │           dep-bin-hello_cargo-a395dae34745bcde
        │           invoked.timestamp
        │
        ├───build
        ├───deps
        │       hello_cargo-a395dae34745bcde.d
        │       hello_cargo-a395dae34745bcde.exe
        │       hello_cargo-a395dae34745bcde.pdb
        │
        ├───examples
        └───incremental
            └───hello_cargo-22f3bxmqxbfgr
                │   s-fiqu004mlt-oglb32.lock
                │
                └───s-fiqu004mlt-oglb32-140ltojrvnqu3
                        1u61dt6owvp097js.o
                        2dx4eoeffqq8ely7.o
                        3ws2uvgmoh0tnkqn.o
                        4fgpioc2zyfydswo.o
                        58xt47pe0vk38jpg.o
                        dep-graph.bin
                        kvbkhulsununltn.o
                        query-cache.bin
                        work-products.bin
```
- Executable file at `.\target\debug\hello_cargo.exe`.
- `Cargo.lock` at top level keeps track of exact version of project dependencies. Never manually edit this file, Cargo manages it.
- `--release` flag compiles the project with optimisations that result in a slower compilation but faster executable. Always use `--release` flag for profiling and production releases. E.g.:
    ```
    PS C:\Users\peter\Documents\rust-projects\hello_cargo> cargo build --release
    Compiling hello_cargo v0.1.0 (C:\Users\peter\Documents\rust-projects\hello_cargo)
    Finished release [optimized] target(s) in 0.36s
    ```
    Adds the `.\target\release\` directory:
    ```
    ...
    └───target
        │
        ...
        │
        └───release
                │   .cargo-lock
                │   hello_cargo.d
                │   hello_cargo.exe
                │   hello_cargo.pdb
                │
                ├───.fingerprint
                │   └───hello_cargo-147a78feb613f770
                │           bin-hello_cargo-147a78feb613f770
                │           bin-hello_cargo-147a78feb613f770.json
                │           dep-bin-hello_cargo-147a78feb613f770
                │           invoked.timestamp
                │
                ├───build
                ├───deps
                │       hello_cargo-147a78feb613f770.d
                │       hello_cargo-147a78feb613f770.exe
                │       hello_cargo-147a78feb613f770.pdb
                │
                ├───examples
                └───incremental
    ```

### [`cargo run`][8]
> Run the current package
- Will compile the package if necessary.

### [`cargo check`][9]
> Check a local package and all of its dependencies for errors. This will essentially compile the packages without performing the final step of code generation, which is faster than running `cargo build`.
- Allows for faster dev iteration with frequent code checking.

[1]: https://doc.rust-lang.org/book/ch01-03-hello-cargo.html
[2]: https://doc.rust-lang.org/book/title-page.html
[3]: https://doc.rust-lang.org/cargo/commands/cargo-new.html
[4]: https://doc.rust-lang.org/cargo/reference/manifest.html
[5]: https://doc.rust-lang.org/cargo/reference/manifest.html#the-package-section
[6]: https://doc.rust-lang.org/cargo/reference/specifying-dependencies.html
[7]: https://doc.rust-lang.org/cargo/commands/cargo-build.html
[8]: https://doc.rust-lang.org/cargo/commands/cargo-run.html
[9]: https://doc.rust-lang.org/cargo/commands/cargo-check.html 
