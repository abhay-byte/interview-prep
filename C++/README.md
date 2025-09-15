### **C++: 10 Theoretical Questions**

**1. Q: What is RAII (Resource Acquisition Is Initialization)?**
*   **A:** RAII is a core C++ programming idiom where the acquisition of a resource (like memory, a file handle, or a network socket) is tied to the lifetime of an object. The resource is acquired in the object's constructor and automatically released in its destructor. This guarantees that resources are properly cleaned up, even in the presence of exceptions, making code safer and preventing resource leaks. Smart pointers (`std::unique_ptr`, `std::shared_ptr`) are a primary example of RAII.

**2. Q: Explain the differences between `std::unique_ptr`, `std::shared_ptr`, and `std::weak_ptr`.**
*   **A:** These are smart pointers that manage dynamic memory using RAII.
    *   `std::unique_ptr`: Provides exclusive ownership of a resource. It cannot be copied, only moved. The resource is deallocated when the `unique_ptr` goes out of scope.
    *   `std::shared_ptr`: Provides shared ownership of a resource using a reference count. The resource is deallocated only when the last `shared_ptr` pointing to it is destroyed.
    *   `std::weak_ptr`: A non-owning "observer" of a `shared_ptr`. It holds a weak reference that does not increase the reference count. It is used to break circular dependency cycles between `shared_ptr` instances.

**3. Q: What is "The Rule of Three/Five/Zero"?**
*   **A:** This is a guideline for C++ class design concerning resource management.
    *   **Rule of Three:** If a class defines any of a destructor, copy constructor, or copy assignment operator, it should probably define all three.
    *   **Rule of Five (C++11):** Extends the Rule of Three. If a class defines any of the original three plus a move constructor or move assignment operator, it should probably define all five.
    *   **Rule of Zero:** The best practice. A class should not manage resources itself but should delegate resource management to dedicated resource-handling classes (like smart pointers and standard library containers), thereby avoiding the need to write any of the five special member functions.

**4. Q: How is runtime polymorphism implemented in C++?**
*   **A:** Runtime polymorphism is implemented using **virtual functions** and a mechanism called a **virtual table (vtable)**. When a class declares a virtual function, the compiler creates a vtable for that class, which is a lookup table of function pointers. Each object of that class contains a hidden pointer (the **vptr**) to this vtable. When a virtual function is called through a base class pointer, the program uses the vptr at runtime to find the correct vtable and call the appropriate overridden function in the derived class.

**5. Q: What is the difference between stack and heap memory allocation?**
*   **A:**
    *   **Stack:** An area of memory for static allocation, used for local variables and function call management. Allocation and deallocation are extremely fast (just moving a stack pointer) and are managed automatically by the compiler. Memory is limited, and variables are destroyed when they go out of scope.
    *   **Heap:** An area of memory for dynamic allocation. It is used for objects whose lifetime must extend beyond the scope of a single function. Allocation (using `new`) and deallocation (using `delete`) are slower and must be managed manually by the programmer (or via smart pointers). The heap is much larger but risks memory leaks if not managed correctly.

**6. Q: What are templates in C++?**
*   **A:** Templates are the foundation of generic programming in C++. They allow you to write functions and classes that can operate with any data type without having to write separate versions for each type. The compiler generates the specific version of the class or function when it is used with a particular type, promoting code reuse and type safety. The Standard Template Library (STL) is built entirely on this concept.

**7. Q: Explain the importance of `const` correctness.**
*   **A:** `const` correctness is the practice of using the `const` keyword to prevent unintentional modification of data. It serves as a contract that a function will not change its parameters or, if it's a member function, will not change the state of the object. This makes code safer, easier to reason about, and self-documenting. It also allows the compiler to perform certain optimizations and is crucial for working with temporary objects and constant references.

**8. Q: What are rvalue references and what problem do they solve?**
*   **A:** An **rvalue reference** (denoted by `&&`) is a reference that can bind to a temporary object (an rvalue) that is about to be destroyed. They are the core feature that enables **move semantics**. The problem they solve is the expensive and unnecessary copying of temporary objects. Instead of copying the data from a temporary object, the resources (like a pointer to heap memory) to be "stolen" or "moved" from the temporary object to a new object, avoiding a deep copy.

**9. Q: What is the Standard Template Library (STL)?**
*   **A:** The STL is a core part of the C++ Standard Library. It provides a collection of generic classes and functions. Its three main components are:
    *   **Containers:** Data structures that store objects (e.g., `std::vector`, `std::map`, `std::list`).
    *   **Algorithms:** Procedures that operate on containers (e.g., `std::sort`, `std::find`, `std::copy`).
    *   **Iterators:** Objects that act like pointers, providing a common way for algorithms to traverse through the elements of different container types.

**10. Q: What is Undefined Behavior (UB)?**
*   **A:** Undefined Behavior is behavior that results from executing code whose semantics are not defined by the C++ language specification. This can happen from actions like dereferencing a null pointer, accessing an array out of bounds, or a signed integer overflow. When UB occurs, the program is invalid, and the C++ standard places no requirements on what must happen—it might crash, it might produce incorrect results, it might appear to work correctly, or it might format your hard drive. It is one of the most dangerous aspects of C++.