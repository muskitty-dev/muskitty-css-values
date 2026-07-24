# muskitty-css-values

[English](README.md) | [简体中文](README.zh-CN.md)

[![crates.io](https://img.shields.io/crates/v/muskitty-css-values.svg)](https://crates.io/crates/muskitty-css-values)
[![Documentation](https://docs.rs/muskitty-css-values/badge.svg)](https://docs.rs/muskitty-css-values)
[![License](https://img.shields.io/crates/l/muskitty-css-values.svg)](https://github.com/muskitty-dev/muskitty-css-values/blob/main/LICENSE)

A typed CSS value parser implementing [CSS Values Level 4](https://drafts.csswg.org/css-values-4/)
and [CSS Variables Level 1](https://drafts.csswg.org/css-variables-1/), built on
[`muskitty-css-parser`](https://crates.io/crates/muskitty-css-parser).

Part of the [MusKitty](https://github.com/muskitty-dev) browser engine project.

## Status

| Component | Spec | Tests |
|-----------|------|-------|
| Numeric types (Length/Angle/Time/...) | CSS Values §4.4-§4.7, §5, §6 | 33 |
| Textual types (Keyword/Ident/String/Url) | CSS Values §3 | 25 |
| Math expressions (calc/min/max/clamp) | CSS Values §9 | 36 |
| var() references | CSS Variables §2-§3 | 12 |
| Grammar hooks + serialization | CSS Values §5.4.1, §8.1, §9.7 | 33 |
| **Total** | | **148** |

- Zero `unsafe` code
- Zero C/C++ dependencies
- Runtime dependency: `muskitty-css` (facade over tokenizer + parser)
- Rust stable toolchain only
- MSRV 1.82

## Installation

```toml
[dependencies]
muskitty-css-values = "0.1.0"
```

## Quick Start

```rust
use muskitty_css_values::{parse_value, CssValue};

let val = parse_value("calc(100% - 2em)").unwrap();
// CssValue::Math(MathExpression::Sum(...))
```

## Architecture

```
muskitty-css-values/
  src/
    lib.rs              Public API + re-exports
    numeric.rs          Length/Percentage/Number/Integer/Angle/Time/
                        Frequency/Resolution/Ratio (§4.4-§4.7, §5, §6)
    textual.rs          Keyword/CustomIdent/DashedIdent/CssString/Url (§3)
    math.rs             MathExpression AST + calc/min/max/clamp parser (§9)
    var.rs              VarReference parsing (CSS Variables §3)
    grammar.rs          ValuesGrammar impl Grammar trait (§5.4.1)
    serialize.rs        ToCss trait + serialization (§8.1, §9.7)
  tests/
    5 test files, 148 tests total
```

## Design Principles

1. **Parse, don't compute** — This crate builds typed ASTs. Numeric
   resolution, var() substitution, and calc() evaluation happen in the
   cascade layer.
2. **CSSWG is ground truth** — Implementation follows the spec exactly.
3. **Zero unsafe** — Pure safe Rust.

## License

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.

Copyright 2026 MusCat / MusKitty Bit-Torch Community
