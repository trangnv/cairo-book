# Installation

_Currently v1.0.0-alpha.6_

## Prerequisites

- Install [Rust](https://www.rust-lang.org/tools/install)
- Setup Rust:

```bash
rustup override set stable && rustup update
```

## Clone Cairo 1.0 compiler

Clone the repository locally

```bash
git clone https://github.com/starkware-libs/cairo
```

## Build the repository

```bash
cd cairo
cargo build --all --release
cd target/release
run pwd # to know the path to the binaries (e.g. starknet-compile)
```

## Add the release directory to PATH

- Open `~/.zshrc` or `~/.bashrc` (depending your shell)
- Add the following line to the end of the file:

```bash
export PATH="<PATH_TO_CAIRO_COMPILER>"
```

e.g.

```bash
export PATH="/Users/username/cairo/target/release"
```

- Save the change and restart terminal.
- To check run

```bash
which starknet-compile
```

Should see the path to the Cairo 1.0 repo printed!, `/Users/username/cairo/target/release/cairo-compile`
