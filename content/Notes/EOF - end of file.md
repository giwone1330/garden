---
tags:
  - CPP
  - PS
  - Python
---
## End of File
There are cases where you would like a program to do something when you are done giving undetermined length of inputs.

### C++
`std::cin.eof()` this returns `true` if the program reads EOF.
Usage example
```cpp
#include <iostream>
using namespace std;

int main(void)
{
	while (true)
	{
		if (cin.eof())
			break
		else
		{
			; //do something here
		}
	}
}
```
For the case of Linux (Windows WSL), you may input `ctrl + d` to input EOF to the console.
### Python
To the best of my knowledge, python does not have a `std::cin.eof()` equivalent, however it can perform similarly as the above example
```python
import sys

for line in sys.stdin: # each `line` is the string of raw input line
	pass # do something here
```
Giving EOF input to the console is same as the case of C++, input `ctrl + d`.
