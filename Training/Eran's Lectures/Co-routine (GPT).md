
Coroutines in C++ are a language feature introduced in C++20 that allow you to write asynchronous code in a more readable and sequential manner. 
They provide a way to suspend and resume execution of a function at specific points, without blocking the entire thread.

Here's a step-by-step explanation of how coroutines work in C++:

1. Coroutine Keywords: C++20 introduces three new keywords related to coroutines:
    
    - `co_await`: This keyword is used to suspend the execution of a coroutine and wait for the completion of another coroutine or asynchronous operation.
    - `co_yield`: This keyword is used to suspend the execution of a coroutine and produce a value that can be retrieved by the caller.
    - `co_return`: This keyword is used to terminate the execution of a coroutine and return a value to the caller.
2. Coroutine Function Declaration: To define a coroutine, you need to declare it with the `async` keyword and specify its return type as a coroutine type. A coroutine function is defined like any other function, but it can use the coroutine keywords mentioned above.
    
    For example, here's a simple coroutine function that suspends and yields a sequence of numbers:
    
```cpp
#include <iostream> #include <experimental/coroutine>  
// Coroutine declaration std::experimental::coroutine_handle<> generator;

std::experimental::suspend_always sequence(int start, int end) {    
	for (int i = start; i <= end; ++i) {         
			co_yield i;     
	} 
}
```
    
3. Coroutine Type: The return type of a coroutine function is a coroutine type. This type represents the state of the coroutine and controls its execution. C++20 provides `std::experimental::coroutine_handle<>` as the coroutine type. It acts as a handle to the coroutine's state.
    
4. Coroutine Execution: To execute a coroutine, you need to obtain a coroutine handle and call its `resume()` function. This will start or resume the execution of the coroutine until it reaches a suspend point.
    
    Continuing from the previous example, here's how you can execute the `sequence` coroutine:

```cpp
int main() {     
	// Obtain the coroutine handle     
	generator = sequence(1, 5).coro_handle();
      
	// Resume the coroutine until it completes    
	while (!generator.done()) {        
		generator.resume();         
		int value = generator.promise().value;         
		std::cout << value << std::endl;     
	} 
     
	// Deallocate the coroutine handle     
	generator.destroy();
      
	return 0; 
}
````
``
    
In this example, the coroutine `sequence` is executed in the `main` function. The `resume()` function is called repeatedly until the coroutine is done. Each time `resume()` is called, the coroutine executes until it reaches a `co_yield` statement, at which point it suspends and returns the yielded value.
    
5. Coroutine Promise: The promise is an object associated with each coroutine that is responsible for managing its state and providing its return value. You can access the promise object of a coroutine through the `promise()` function of its handle.
    
    In the previous example, the promise type is not explicitly defined, so the compiler generates a default promise for the coroutine. However, you can define a custom promise type by implementing the necessary functions like `initial_suspend()`, `final_suspend()`, and `return_value()`.
    

Coroutines provide a more readable and structured way to write asynchronous code by allowing you to express sequential logic while hiding the complexities of managing asynchronous operations and callbacks. They are particularly useful in scenarios involving asynchronous I/O, event-driven programming, and other forms of concurrency.