---
tags:
  - CPP
  - PS
---
## Trigraph
In C++, the sequence of two question marks (??) followed by certain characters is known as a trigraph. Trigraphs were used in early C and C++ to provide a way to represent characters that might not be easily typed or displayed on some keyboards and character sets. For example, `??=` represents `#`, `??/` represents `\`, etc.

To output a string with double question marks, you have to split the consecutive question marks to prevent the compiler to interpret them as a trigraph.

```cpp
std::cout << "Hello World?\?"
```