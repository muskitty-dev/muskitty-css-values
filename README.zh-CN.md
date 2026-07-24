# muskitty-css-values

[English](README.md) | [简体中文](README.zh-CN.md)

纯 Rust 实现的 CSS 类型化值解析器，遵循 [CSS Values Level 4](https://drafts.csswg.org/css-values-4/)
和 [CSS Variables Level 1](https://drafts.csswg.org/css-variables-1/)。

[MusKitty](https://github.com/muskitty-dev) 浏览器引擎项目的一部分。

## 状态

| 组件 | 规范 | 测试 |
|------|------|------|
| 数值类型 | CSS Values §4.4-§4.7, §5, §6 | 33 |
| 文本类型 | CSS Values §3 | 25 |
| 数学表达式 | CSS Values §9 | 36 |
| var() 引用 | CSS Variables §2-§3 | 12 |
| Grammar hooks + 序列化 | §5.4.1, §8.1, §9.7 | 33 |
| **总计** | | **148** |

- 零 `unsafe` 代码
- 零 C/C++ 依赖
- Rust stable，MSRV 1.82

## 安装

```toml
[dependencies]
muskitty-css-values = "0.1.0"
```

## 设计原则

1. **只解析，不计算** — 本 crate 构建类型化 AST。数值解析、var() 替换、calc() 求值在 cascade 层完成。
2. **CSSWG 是 ground truth**
3. **零 unsafe**

## 许可

Apache License, Version 2.0。详见 [LICENSE](LICENSE)。

Copyright 2026 MusCat / MusKitty Bit-Torch Community
