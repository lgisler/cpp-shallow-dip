# cpp-shallow-dip<a name="cpp-shallow-dip"></a>

https://github.com/lgisler/cpp-shallow-dip

## Table of contents<a name="table-of-contents"></a>

<!-- mdformat-toc start --slug=github --maxlevel=6 --minlevel=1 -->

- [cpp-shallow-dip](#cpp-shallow-dip)
  - [Table of contents](#table-of-contents)
  - [Format](#format)
  - [Language concepts](#language-concepts)
    - [Resource acquisition is initialization](#resource-acquisition-is-initialization)
    - [Stack vs heap memory](#stack-vs-heap-memory)
  - [Core software engineering](#core-software-engineering)
    - [Class & object invariants](#class--object-invariants)
  - [TODO](#todo)

<!-- mdformat-toc end -->

## Format<a name="format"></a>

This document is a collection of _keywords_, _concepts_, _axioms_, _acronyms_, _design patterns_,
and _idioms_ commonly encountered in C++. Using mainly
[cppreference](https://en.cppreference.com/w/) and
[CppCoreGuidelines](https://github.com/isocpp/CppCoreGuidelines/) as references. In general the
sections and topics are ordered from most important to least important but no strict ordering is
applied.

The target audience for this document is mid-level C++ developers looking at learning,
self-improvement, and progressing towards becoming a senior C++ developer.

## Language concepts<a name="language-concepts"></a>

### Resource acquisition is initialization<a name="resource-acquisition-is-initialization"></a>

RAII is an idiom where constructors acquire resources and destructors release them. This means
resources - such as [heap memory](#stack-vs-heap-memory), threads, open sockets, files, locked
mutexes, disk space, database connections - are tied to the lifetime of an object. By making
resource availability a [class invariant](#class--object-invariants), RAII guarantees that all
resources are released when their their controlling objects are destroyed, in reverse order of
acquisition.

Key practices for RAII:

- Encapsulate each resource into a class:
  - The constructor acquires the resource and ensures all class invariants, throwing an exceptions
    if it cannot do so.
  - The destructor releases the resource and must never throw exceptions.
- Ensure that instances of your RAII class:
  - Are created as local variables (automatic storage) or temporaries, or
  - Have a lifetime that does not exceed that of a local or temporary object.

The C++ standard library provides many RAII classes that manage resources automatically. Common
examples include:

- Memory management:
  - [`std::string`][std_string], [`std::vector`][std_vector], [`std::unique_ptr`][std_unique_ptr],
    [`std::shared_ptr`][std_shared_ptr] (manage dynamically-allocated memory)
- File and stream I/O:
  - [`std::fstream`][std_fstream], [`std::stringstream`][std_stringstream]
- Mutex management:
  - [`std::lock_guard`][std_lock_guard], [`std::unique_lock`][std_unique_lock],
    [`std::scoped_lock`][std_scoped_lock], [`std::shared_lock`][std_shared_lock]
- Thread management:
  - [`std::thread`][std_thread], [`std::jthread`][std_jthread] (since C++20)

CppCoreGuidelines rules regarding RAII:

-

### Stack vs heap memory<a name="stack-vs-heap-memory"></a>

## Core software engineering<a name="core-software-engineering"></a>

### Class & object invariants<a name="class--object-invariants"></a>

## TODO<a name="todo"></a>

| #   | Category                        | Key Items & Explanations                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --- | ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Language Core Concepts          | **RAII** (Resource Acquisition Is Initialization); **Object Lifetime & Ownership**; Constructors/Destructors; Copy/Move Semantics; Slicing; Stack vs Heap; Smart Pointers (`unique_ptr`, `shared_ptr`, `weak_ptr`); Manual memory management (`new`, `delete`); OOP (Encapsulation, Inheritance, Polymorphism); Abstraction; Abstract Classes.                                                                                                                  |
| 2   | Core Software Engineering       | **Class & Object Invariants** (Conditions that must always hold true for an object instance); **Preconditions/Postconditions** (for functions/methods); **Assertions** (`assert`); **Design by Contract (DbC)** (documenting & enforcing invariants, pre/postconditions); **Exception Safety Guarantees**; Immutability; Defensive Programming; Testing.                                                                                                        |
| 3   | Key Language Keywords           | `class`, `struct`, `namespace`, `public`, `protected`, `private`, `virtual`, `override`, `final`, `const`, `constexpr`, `consteval`, `constinit`, `template`, `typename`, `inline`, `static`, `mutable`, `this`, `decltype`, `auto`, `using`, `enum`, `enum class`, `explicit`, `friend`, `operator`, `throw`, `try`, `catch`, `noexcept`, `new`, `delete`, `nullptr`, `default`, `delete`, `if constexpr`, `co_await`, `co_return`, `co_yield`, `thread_local` |
| 4   | Templates & Generic Programming | Templates (classes/functions); Template Specialization / Partial Specialization; **SFINAE** (Substitution Failure Is Not An Error); **Concepts** (from C++20 - constraints on type parameters); Templated Lambdas; **CRTP** (Curiously Recurring Template Pattern); Type traits (`std::enable_if`, `std::is_same`, etc.); Variadic Templates.                                                                                                                   |
| 5   | Modern C++ Features             | Move Semantics, `std::move`, Rvalue/lvalue references (`&&`, `&`); Lambda Expressions; Range-based For; Type Deduction (`auto`, `decltype`, `decltype(auto)`); Uniform Initialization (`{}`); Initializer Lists; Smart Pointers; `std::optional`, `std::variant`, Structured Bindings, `std::string_view`, Ranges (C++20), Span, Filesystem.                                                                                                                    |
| 6   | STL & Standard Library Usage    | Containers (`vector`, `deque`, `list`, `map`, `set`, `unordered_map`, etc.); Iterators; Algorithms (`std::sort`, `std::find`, etc.); Allocators; Ranges and Views; Function objects; `std::function`; `std::bind`; `std::chrono` for timing; Allocators; Exception classes; Comparators and Hashing.                                                                                                                                                            |
| 7   | Idioms, Laws & Patterns         | **Rule of 3/5/0** (copy/move management); **PImpl** (Pointer to Implementation, for ABI stability); **Copy-and-swap**; **Non-Virtual Interface** (NVI); Named Constructors; Singleton/Observer/Factory (classic patterns); Iterator, Proxy, Adapter, Visitor (patterns); Enable If Idiom; Scope Guard; Resource Manager.                                                                                                                                        |
| 8   | Robustness & Exception Safety   | Safe Exception Handling; noexcept; Exception-neutral code; Basic and Strong Exception Guarantees; Try/catch best practices; RAII for resource recovery; Error codes vs exceptions; Custom exception classes; Propagation, translation, and logging of exceptions.                                                                                                                                                                                               |
| 9   | Concurrency & Multithreading    | **Data races and race conditions**; Synchronization primitives (mutex, lock_guard, unique_lock, condition_variable); **std::thread**, **std::async**, **future**, **promise**; Atomics; memory order/type; Thread pools; Lock-free programming; Deadlock avoidance; Double-checked locking.                                                                                                                                                                     |
| 10  | Performance & Optimization      | Inlining; Move/copy elision (RVO, NRVO); Branch prediction; False sharing & cache effects; Memory alignment; Allocator tuning; Microbenchmarking; Value categories (lvalue, xvalue, glvalue, prvalue); Expression templates for perf; Profiling and bottleneck analysis.                                                                                                                                                                                        |
| 11  | Advanced Practices              | Metaprogramming (static_assert, constexpr, template recursion); Type erasure (`std::function`, concepts, vtables); Custom allocators and memory pools; Expression templates; Policy-based design; Mixins; Intrusive containers; Tag dispatch; CRTP-powered customization.                                                                                                                                                                                       |
| 12  | Tooling & Process               | Build systems (`cmake`, `make`); Debugging (gdb, lldb); Static Analysis (clang-tidy, cppcheck); Memory/error sanitizers (ASan, UBSan, TSAN); Profilers (valgrind, perf, Instruments); Documentation (Doxygen, Sphinx); Code Review; Continuous Integration; Test Frameworks (Google Test, Catch2).                                                                                                                                                              |
| 13  | Axioms, Laws, Design Principles | **Zero Overhead Principle**; "Don’t pay for what you don’t use" (Stroustrup); Single Responsibility Principle (SRP); Open/Closed Principle; Liskov Substitution Principle (LSP); Law of Demeter; DRY (Don’t Repeat Yourself); KISS; YAGNI; SOLID (SRP, OCP, LSP, ISP, DIP); API/ABI stability.                                                                                                                                                                  |
| 14  | Acronyms                        | **RAII** (Resource Acquisition Is Initialization); **SFINAE**; **CRTP**; **SOLID**; **POD** (Plain Old Data); **API/ABI**; **OOP/OOD** ("Object-Oriented Programming" / "Object-Oriented Design"); **NVI** (Non-Virtual Interface); **RVO/NRVO** (Return/Named Return Value Optimization).                                                                                                                                                                      |
| 15  | Legacy, Interop & Preprocessor  | Header guards, `#pragma once`; Macros (use, dangers, conditional compilation); Preprocessing (`#define`, `#ifdef`); C interop: `extern "C"`, handling name mangling; Include ordering and dependencies; Linking with other languages/libraries.                                                                                                                                                                                                                 |

[std_fstream]: https://en.cppreference.com/w/cpp/io/basic_fstream.html
[std_jthread]: https://en.cppreference.com/w/cpp/thread/jthread.html
[std_lock_guard]: https://en.cppreference.com/w/cpp/thread/lock_guard.html
[std_scoped_lock]: https://en.cppreference.com/w/cpp/thread/scoped_lock.html
[std_shared_lock]: https://en.cppreference.com/w/cpp/thread/shared_lock.html
[std_shared_ptr]: https://en.cppreference.com/w/cpp/memory/shared_ptr.html
[std_string]: https://en.cppreference.com/w/cpp/string/basic_string.html
[std_stringstream]: https://en.cppreference.com/w/cpp/io/basic_stringstream.html
[std_thread]: https://en.cppreference.com/w/cpp/thread/thread.html
[std_unique_lock]: https://en.cppreference.com/w/cpp/thread/unique_lock.html
[std_unique_ptr]: https://en.cppreference.com/w/cpp/memory/unique_ptr.html
[std_vector]: https://en.cppreference.com/w/cpp/container/vector.html
