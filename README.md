pcre2
=====
A high level Rust wrapper library for [PCRE2](https://www.pcre.org/).

[![Build status](https://github.com/BurntSushi/rust-pcre2/workflows/ci/badge.svg)](https://github.com/BurntSushi/rust-pcre2/actions)
[![crates.io](https://img.shields.io/crates/v/pcre2.svg)](https://crates.io/crates/pcre2)

Dual-licensed under MIT or the [UNLICENSE](https://unlicense.org/).


### Documentation

https://docs.rs/pcre2


### Usage

Run `cargo add pcre2` to add this crate to your `Cargo.toml` file.


### Notes

Currently, this is a fairly light layer around PCRE2 itself and does not even
come close to covering all of its functionality. There are no specific plans
in place to build out the wrapper further, but PRs for making more of PCRE2
available are welcome, although my bandwidth for maintenance is limited. If
you're interested in sharing this maintenance burden, please reach out.


### WebAssembly

`pcre2` and `pcre2-sys` can be compiled to WebAssembly on `wasm32-wasip1`
(and its variants). JIT is automatically disabled on `wasm32`/`wasm64`
targets because sljit has no WebAssembly backend. `wasm32-unknown-unknown`
is not supported out of the box: PCRE2 is written in C and requires a libc,
which that target does not provide.

To build, install [wasi-sdk](https://github.com/WebAssembly/wasi-sdk) and
point `cc` at it. For example:

```sh
# One-time setup
rustup target add wasm32-wasip1
# Install wasi-sdk to $WASI_SDK (e.g. ~/.local/wasi-sdk)

export CC_wasm32_wasip1="$WASI_SDK/bin/clang"
export AR_wasm32_wasip1="$WASI_SDK/bin/llvm-ar"
cargo build --target wasm32-wasip1 --release
```

Tests can be run with a WASI runtime such as
[wasmtime](https://wasmtime.dev/):

```sh
CARGO_TARGET_WASM32_WASIP1_RUNNER=wasmtime \
  cargo test --target wasm32-wasip1 --release
```
