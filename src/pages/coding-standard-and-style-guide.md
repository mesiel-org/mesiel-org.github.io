---
title: Mesiel Coding Standard & Style Guide
toc: true
layout: ../layouts/Layout.astro
---

## 1. Scope and Purpose
This document defines the Mesiel Coding Standard and Style Guide. All source code within Mesiel projects shall conform to this standard. The goals are clarity, safety, predictability, performance, and consistency across the code base. This standard applies equally to C, C++, and similar system-level languages. It may be adapted for other languages.

## 2. General Principles
- Code shall be written for long-term readability.  
- Code shall avoid ambiguity.  
- Code shall be deterministic where possible.  
- Performance shall be considered at every stage, but not at the cost of safety or readability.  
- Undefined or unspecified behavior is forbidden.  
- Code must be written in a way that can be verified by human review.

## 3. File Organization
- Each file shall contain a single, clear purpose.  
- Source files shall use the extension `.c` or `.cc`. Header files shall use `.h` or `.hh`.  
- Headers shall always have include guards in the form `#ifndef NAME_H` / `#define NAME_H` / `#endif`.  
- A file shall begin with a comment describing its purpose.  
- Order within a file: includes, defines, global declarations, type declarations, function declarations, function definitions.

Example minimal include guard:
```
#ifndef EXAMPLE_H
#define EXAMPLE_H

/* contents */

#endif /* EXAMPLE_H */
```

## 4. Naming Conventions
- Identifiers shall be descriptive and unambiguous.  

- Global variables are forbidden, expect for constants.

- Member variables shall be prefixed with `m_`. Example: `m_count`.  

- Constants shall be all uppercase with underscores. Example: `MAX_VALUE`.  

- Functions and procedures shall use lowercase with underscores. Example: `compute_sum`.  

- Types and Classes shall use PascalCase. Example: `FileReader`. 

- File names shall be all lowercase with underscores. Example: `file_reader.c`.  

- Short or cryptic names are forbidden except in loop indices (`i`, `j`, `k`).

## 5. Indentation and Layout
- Indentation shall be 4 spaces. Tabs are forbidden.  
- Lines shall not exceed 80 characters, except where unavoidable.  
- One statement per line is mandatory.  
- Whitespace shall be used to improve readability but never inconsistently.

Example:
```
if (x > 0) {
    process(x);
}
```

## 6. Braces and Brackets
- Braces shall always be used, even for single-line statements.  
- For functions, the opening brace shall be on the next line.  
- For control structures, the opening brace shall be on the same line.  
- Closing braces shall align with the beginning of the construct.

Example for functions:
```
int add(int a, int b)
{
    return a + b;
}
```

Example for control structures:
```
if (a > b) {
    swap(a, b);
}
```

## 7. Comments and Documentation
- All files, functions, structures, and global symbols shall be documented with Doxygen.  
- Comments shall describe intent, not mechanics.  
- Inline comments shall be used sparingly.  
- Obsolete comments shall be removed.  
- Documentation shall be maintained as part of the code.

Example:
```
/**
 * Compute the sum of two integers.
 * @param a First integer.
 * @param b Second integer.
 * @return Sum of a and b.
 */
int compute_sum(int a, int b);
```

## 8. Declarations and Definitions
- All variables shall be declared at the smallest possible scope.  
- Initialization shall occur at declaration where possible.  
- Forward declarations shall be used instead of unnecessary includes.  
- Variables shall never be reused for multiple unrelated purposes.

Example:
```
for (int i = 0; i < n; i++) {
    total += array[i];
}
```

## 9. Constants, Literals, and Macros
- Constants shall be defined using `const` or `enum`.  
- Macros shall be avoided unless absolutely required (e.g., include guards).  
- Magic numbers are forbidden.  
- Literals shall be typed explicitly when necessary (e.g., `0u` for unsigned).

## 10. Expressions and Statements
- Expressions shall be simple and avoid hidden side effects.  
- The result of an assignment shall not be used within another expression.  
- Increment and decrement operators shall not be used within larger expressions.  
- Boolean expressions shall be explicit.

Forbidden:
```
if (a = b) { ... }
```

Required:
```
a = b;
if (a) { ... }
```

## 11. Control Structures
- `if`, `for`, `while`, and `switch` shall always use braces.  
- `switch` statements shall always include a `default` case.  
- Fallthrough in `switch` is forbidden unless explicitly commented.  
- Loops shall have a clear termination condition.  
- `goto` is forbidden except for controlled cleanup.

Example:
```
switch (value) {
case 1:
    handle_case1();
    break;
case 2:
    handle_case2();
    break;
default:
    handle_default();
    break;
}
```

## 12. Functions and Procedures
- Functions shall be short and do one thing.  
- Maximum function length: 50 lines.  
- Function names shall be descriptive.  
- Functions shall not exceed 5 parameters.  
- Functions shall document all parameters and return values.  
- Functions shall return status codes or errors explicitly, not implicitly.

## 13. Structures, Classes, and Objects
- Structures and classes shall group related data only.  
- All members shall be explicitly initialized.  
- Public interface shall be minimal.  
- Data hiding is mandatory; implementation details shall not leak.  
- Multiple inheritance is forbidden.  
- Virtual inheritance is forbidden unless strictly required.

## 14. Memory Management
- Memory allocation and deallocation must always be paired.  
- Ownership of allocated memory shall be explicit.  
- Manual memory management shall be minimized.  
- Memory leaks are forbidden.  
- Use of raw pointers is discouraged; but when used, ownership rules shall be clear.  
- Dynamic allocation shall be avoided in performance-critical paths.

## 15. Error Handling
- All errors shall be checked and handled.  
- Return values of functions shall never be ignored unless explicitly void.  
- Error handling shall not be hidden.  
- Exceptions are forbidden unless the entire project uses them consistently.  
- Status codes are the preferred method.

## 16. Concurrency and Parallelism
- Shared data must be protected by synchronization primitives.  
- Deadlocks are forbidden; code must be designed to prevent them.  
- Race conditions are forbidden.  
- Threads must be joined or detached before program exit.  
- Use of volatile shall be justified and documented.

## 17. Input and Output
- Input shall always be validated.  
- Buffer overflows are forbidden.  
- Output shall be checked for errors.  
- Logging shall be minimal in performance-critical paths.  
- All I/O functions shall be checked for return values.

## 18. Performance Rules
- Complexity of algorithms shall be considered.  
- Unnecessary memory allocations are forbidden.  
- Inline functions shall be used only where they improve performance.  
- Standard library functions shall be used unless performance requires custom implementation.  
- Caching shall be applied cautiously.  
- Premature optimization is forbidden, but performance regression is also forbidden.

## 19. Safety Rules
- Null pointer dereference is forbidden.  
- Array bounds must always be checked.  
- Type casting shall be explicit and minimized.  
- Dangerous functions such as `gets` are forbidden.  
- Integer overflow and underflow shall be avoided and checked.  
- Assertions shall be used to enforce invariants.

## 20. Portability Rules
- Code shall compile cleanly on all supported compilers.  
- Compiler-specific extensions are forbidden.  
- Behavior shall not depend on endianness or word size unless explicitly documented.  
- All assumptions about the environment shall be documented.

## 21. Testing and Verification
- Every module shall have corresponding tests.  
- Unit tests shall be automated.  
- Test coverage shall include edge cases.  
- Tests shall be reproducible and deterministic.  
- Undefined or unspecified behavior in tests is forbidden.

## 22. Closing Notes
The Mesiel Coding Standard and Style Guide is mandatory for all code contributions. Code not conforming shall be rejected. The purpose is uniformity, safety, performance, and long-term maintainability. The rules apply strictly, and exceptions are not allowed unless formally approved.
