---
tags:
  - CPP
  - PS
---
## Output Precision
When outputting decimal values such as `float` or `double` using `std::cout` it doesn't print with full precision. By default, C++ seems to output precision of 6 digits. So if the problem requires higher precision, you can do so by specifying the format and setting the precision to your liking.

```cpp
std::cout << std::fixed;
std::cout.precicsion(user_precision)
```