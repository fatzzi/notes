### `std::function`

`std::function` provides a type-safe (ensures the callable object matches the expected signature) way to store and invoke all callable objects like functions, function pointers, lambda expressions, and functors. It is defined in the `<functional>` header.

Think of it as a box that can hold anything that behaves like a function and lets you call it later.

## Syntax

```cpp
#include <functional>

std::function<return_type(parameter_types)> functionName;
std::function<int(int, int)> op;  // A callable that takes two ints and returns an int
```
## lambda
``` cpp
std::function<void()> sayHello = []() {
    std::cout << "Hello!" << std::endl;
};
sayHello();  // Call the lambda
```

## Storing Function Pointer

```cpp
int add(int a, int b) { return a + b; }

std::function<int(int, int)> op = add;
std::cout << op(3, 4);  // Output: 7
```

This is actually in terms of output equivalent to:

``` cpp
int (*funcPtr)(int, int);
funcPtr = add; // or funcPtr = &add; (the & is optional)
```

But under the hood they are very different. std::function can store all callable objects while a normal raw function cannot. For example, we have a lambda:

```cpp
int x = 5;
auto lambda = [x](int a) {
    return a + x;
};
```

Since it captures x, you cannot store this in a function pointer. In std::function<int(int)>, however, can store it. Following are some examples of how std::function can be used.


## Key Points:
- Type Erasure: Can hold any callable type matching a specific signature.
- Type Safety: Ensures only compatible callables can be assigned.
- Copyable and Assignable: Easy to pass around in code.
- Storage: Manages both small and large callable objects.
- std::function may introduce some overhead compared to function pointers or direct calls due to heap allocation.

## Summary
std::function in C++ is a type-safe, general-purpose function wrapper that can store anything callable—like regular functions, lambda expressions (even with captures), function pointers, or functors (objects with operator()). It's defined in the <functional> header and allows you to treat different kinds of callable entities uniformly. For example, std::function<int(int, int)> func; can hold any function that takes two int arguments and returns an int. You can assign it like func = [](int a, int b) { return a + b; }; and call it with func(2, 3). Unlike function pointers, std::function supports lambdas with captures and is more flexible, though it introduces a slight overhead due to type erasure and heap allocation in some cases.

For more examples on how std::function is used check out [examples]()!
