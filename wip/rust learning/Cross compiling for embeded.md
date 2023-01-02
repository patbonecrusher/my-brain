---
creation date: 2022-12-25 09:38
modification date: Sunday, 25th December 2022, 09:38:58
tags: [engineering, engineering/language/rust, engineering/embedded]
---

# Cross compiling for embeded

## Goal

To cross compile a hello world to an embedded platform.

```
rustup target add arm-unknown-linux-musleabi
cargo build --target=arm-unknown-linux-musleabi

>> FAILED.
```

## Next

Figure out how to pass in the path to a compiled.  Need to install the gcc toolchain.
