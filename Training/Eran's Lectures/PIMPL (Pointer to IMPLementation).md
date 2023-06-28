
### In Regatta we are using PimplWrapper class for it

### ChatGPT
PIMPL is an idiom in C++ that is used to hide the implementation details of a class from its users. It is also known as the "Opaque Pointer" or "Compiler Firewall" idiom.

The main idea behind PIMPL is to separate the public interface of a class from its private implementation. Instead of exposing the implementation details directly in the class header file, the PIMPL idiom introduces a level of indirection. The public class contains a pointer to a private implementation class, and the actual implementation details are kept in a separate source file.

### Example

**MyClass.h (public header file)**

cppCopy code

```cpp
class MyClass { 
public:     
	MyClass();    
	~MyClass();      
	void doSomething();  
private:     
	class Impl;  // Forward declaration of the private implementation class     
	Impl* pImpl; // Pointer to the private implementation 
};
```

**MyClass.cpp (source file)**

cppCopy code

```cpp
#include "MyClass.h"  
class MyClass::Impl { 
public:     
void privateFunction() {         
		// Implementation details     
	} 
}; 

MyClass::MyClass() : pImpl(new Impl()) {}  

MyClass::~MyClass() {     
	delete pImpl; 
}  

void MyClass::doSomething() {     
	pImpl->privateFunction(); 
}

```

In this example, the public header file `MyClass.h` only contains the public interface of the class `MyClass`. The private implementation details are hidden in the `MyClass::Impl` class, which is defined in the `MyClass.cpp` source file.

By using the PIMPL idiom, the implementation details can be modified independently without affecting the public interface. This can provide benefits such as better encapsulation, reduced compilation dependencies, and easier library versioning and binary compatibility.

Additionally, the PIMPL idiom can help improve build times since changes to the implementation details don't require recompilation of the code that depends on the class.
