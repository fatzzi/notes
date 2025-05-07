# Examples for std::function
 
## 1. Storing a Lambda (No Capture)
```cpp

std::function<void()> sayHello = []() {
    std::cout << "Hello!" << std::endl;
};
sayHello();  // Output: Hello!

```
This lambda has no parameters or captures and fits std::function<void()>.

## 2. Storing a Function Pointer
```cpp

int add(int a, int b) { return a + b; }

std::function<int(int, int)> op = add;
std::cout << op(3, 4);  // Output: 7
```
A regular function can be stored in a std::function as long as the signature matches.

### Function Pointer Version:
```cpp

int (*funcPtr)(int, int) = add;
```
std::function is more flexible since it can also store lambdas with captures or functors.

## 3. Storing a Lambda with Capture
```cpp

int x = 5;
auto lambda = [x](int a) {
    return a + x;
};

std::function<int(int)> f = lambda;
std::cout << f(10);  // Output: 15

```
This lambda captures x by value. You can't store it in a raw function pointer, but std::function can handle it.

## 4. Using std::function with STL Algorithm
```cpp

std::vector<int> numbers = {1, 2, 3, 4, 5};

std::function<void(int)> print = [](int x) {
    std::cout << x << " ";
};

std::for_each(numbers.begin(), numbers.end(), print);
// Output: 1 2 3 4 5
```

std::function works perfectly with algorithms expecting callables like std::for_each.

#3 5. Changing Function at Runtime
```cpp
std::function<int(int, int)> operation;

operation = [](int a, int b) { return a + b; };
std::cout << operation(2, 3) << std::endl; // Output: 5

operation = [](int a, int b) { return a * b; };
std::cout << operation(2, 3) << std::endl; // Output: 6
```
You can reassign different behaviors to the same std::function object.

## 6. Passing std::function to a Function (Callback)
```cpp

void compute(int a, int b, std::function<int(int, int)> func) {
    std::cout << "Result: " << func(a, b) << std::endl;
}

compute(5, 3, [](int x, int y) { return x - y; });  // Output: Result: 2
```
compute is a function that takes:
- Two int values: a and b
- A callable object func that matches the signature int(int, int)
Inside compute, it simply calls func(a, b) and prints the result.



