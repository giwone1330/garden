---
tags:
  - Python
  - Study
  - PS
  - CPP
---
## Time Limit
When doing PS (Problem Solving) or LC (LeetCode), all of the problems have time limit. The time limit exists to prevent brute forcing or to suggest the degree of efficiency for the submitted solutions. However there are cases where input and output stages are the primary bottleneck for this time limit, especially when input and outputs are iterated in the algorithm.

## Fast IO
### Python
```python
import sys

# fast input
problem_input = sys.stdin.readline().rstrip()

# fast output
sys.stdout.write(problem_output)
```

### C++
```cpp
#include <iostream>
using namespace std;

// fast io settings
ios::sync_with_stdio(false);
cin.tie(NULL);
cout.tie(NULL);

// fast input
cin >> problem_input;

// fast output
cout << problem_output;
```

## Calculating the time limit
There is no official statement about this, but usually online judge sites take 1seconds for 100,000,000 operations or iterations (C++). So you may use this information to have a sense of the time limit, and plan your answers accordingly. (Brute forcing may be a viable option depending of the conditions)
- 1 second ~ 100,000,000 operations or iterations
Python is slower than this guideline. See [[C++ vs Python]].