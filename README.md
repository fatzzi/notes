#  Notes on Function Pointers, Lambdas, and `std::function` in C++


This repository contains notes and examples focused on **Function Pointers**, **Lambdas**, and **`std::function`** in C++. These are powerful concepts that every C++ developer should be familiar with, and I’ve compiled this to help others (and myself!) understand them better.

---

## What You'll Find Here

### [Function Pointers](https://github.com/fatzzi/notes/blob/main/Function_Pointers.md)
Function pointers are variables that store the address of a function. They let you:
- Call functions indirectly
- Pass functions as arguments
- Implement callbacks


### [Lambdas](https://github.com/fatzzi/notes/blob/main/Lambda_Expressions.md)
Lambdas in C++ allow you to define anonymous functions on the fly, right where you need them. They can capture variables from their surrounding scope and can be used in place of regular function pointers. Topics include:
- Basic syntax
- Captures by value, reference, and mixed
- Using `mutable` to modify captured values
- Explicit return types and auto return type deduction

### `std::function`
`std::function` is a flexible, type-safe way to store any callable object (functions, function pointers, lambdas, functors). It ensures that the signature matches what’s expected and is easier to use in complex situations where the callable type might change. You’ll learn:
- Storing function pointers and lambdas
- Using it with functors and STL algorithms
- When to use `std::function` vs raw function pointers

---
