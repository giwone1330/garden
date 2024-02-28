---
tags:
  - CPP
  - Programming
  - Python
---
[reference](https://stackoverflow.com/questions/38491212/difference-between-compiled-and-interpreted-languages/38491646#38491646)
## Compiled Languages
### Compiler advantages
- Room for optimization
	- Because compilers can see all the code up-front, they can perform a number of analyses and optimizations when generating code that makes the final version of the code executed faster than just interpreting each line individually.
- Less memory usage
	- Compilers can often generate low-level code that performs the equivalent of a high-level ideas like "dynamic dispatch" or "inheritance" in terms of memory lookups inside of tables. This means that the resulting programs need to remember less information about the original code, lowering the memory usage of the generated program.
- Efficient and fast
	- Compiled code is generally faster than interpreted code because the instructions executed are usually just for the program itself, rather than the program itself plus the overhead from an interpreter.
### Compiler drawbacks
- Lacking high level utility
	- Some language features, such as [[Dynamic typing]], are difficult to compile efficiently because the compiler can't predict what's going to happen until the program is actually run. This means that the compiler might not generate very good code.
- Slow startup
	- Compilers generally have a long "start-up" time because of the cost of doing all the analysis that they do. This means that in settings like web browsers where it's important to load code fast, compilers might be slower because they optimize short code that won't be run many times.

## Interpreted Languages
### Interpreter advantages
- Fast startup
	- Because they can read the code as written and don't have to do expensive operations to generate or optimize code, they tend to start up faster than compilers.
- Support for high level utility
	- Because interpreters can see what the program does as its running, interpreters can use a number of dynamic optimizations that compilers might not be able to see.
### Interpreter drawbacks
- High memory usage
	- Interpreters typically have higher memory usage than compilers because the interpreter needs to keep more information about the program available at runtime.
- Slow execution
	- Interpreters typically spend some CPU time inside of the code for the interpreter, which can slow down the program being run.