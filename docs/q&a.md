1Q: What is the primary goal of the language?
1A: To create a maximally performant programming language focused on achieving the highest possible execution speed while remaining convenient and comfortable for the developer to use personally.

2Q: What is the primary approach to maximizing performance?
2A: A highly optimizing compiler that automatically transforms the source code into the fastest possible machine code.

3Q: Should the compiler use runtime profiling to improve optimization?
3A: Yes. The compiler should be able to collect runtime profiling data and use it to improve subsequent compilations.

4Q: What is the priority when choosing between compilation speed and runtime performance?
4A: Runtime performance has the highest priority, even if compilation takes significantly longer.

5Q: How aggressively should the compiler optimize programs?
5A: The compiler should optimize as aggressively as possible, even if the generated machine code differs radically from the source code's structure, provided that the program's observable behavior remains unchanged. The source language should retain strict syntax and explicit semantics without requiring the programmer to manually optimize every operation.

6Q: How explicit should the language syntax be?
6A: The syntax should prioritize maximum explicitness. Types, operations, and program behavior should be clear from the source code, with minimal hidden behavior and implicit operations.

7Q: Should variable and function parameter types be explicitly declared?
7A: Yes. Every variable and function parameter must have an explicitly declared type. The compiler must not infer their types automatically.

8Q: Should the language allow implicit type conversions?
8A: No. All type conversions must be explicit. If an operation involves incompatible types, the programmer must explicitly convert the values to compatible types.

9Q: How should memory management work?
9A: The programmer should have explicit control over memory, while the compiler checks memory usage rules and rejects code that violates them.

10Q: How strictly should the compiler check memory safety?
10A: The compiler should strictly check memory ownership and lifetimes, rejecting code that violates the language's memory safety rules.

11Q: Should the language support unsafe low-level operations?
11A: Yes. The language should provide an explicit unsafe mode for low-level operations that cannot satisfy the normal compiler-enforced memory safety rules. The programmer is responsible for their correctness within unsafe code.

12Q: How should the compiler handle references to objects whose lifetime ends when a function returns?
12A: The compiler must reject references that would outlive the objects they refer to. It must not implicitly extend object lifetimes to make such references valid.

13Q: How should functions access data owned by the caller?
13A: By default, functions should receive temporary access to data without taking ownership. The caller retains ownership and explicitly controls the original data's lifetime and management.

14Q: How should the language restrict simultaneous access to the same data?
14A: Multiple simultaneous read-only accesses to the same data are allowed, but simultaneous mutation of the same data is forbidden unless explicitly synchronized.

15Q: Should the compiler automatically parallelize code?
15A: The compiler should automatically parallelize code only when it can guarantee that doing so is safe and preserves the program's observable behavior.

16Q: How should runtime errors be handled?
16A: The language must use explicit error values instead of exceptions. Functions that can fail must communicate errors through their return values, and the language should require errors to be handled explicitly.

17Q: How should mutability be handled?
17A: Data should be mutable by default. Immutability must be explicitly declared when modifications should be prohibited.

18Q: How should the language support multithreading?
18A: The language should provide both low-level thread management with explicit synchronization and high-level concurrency abstractions for convenient task scheduling and parallel execution.

19Q: Which integer sizes should the initial version of the language support?
19A: The initial version should support fixed-width signed and unsigned integers of 8, 16, 32, and 64 bits. Other integer sizes may be considered in the future.

20Q: How should integer overflow be handled?
20A: The programmer must explicitly choose the overflow behavior for each integer variable. Checked arithmetic must report overflow as an explicit error. Wrapping arithmetic must wrap around at the type's numeric boundaries. The language must never silently choose an overflow policy.

21Q: How should checked arithmetic be implemented?
21A: The compiler must insert runtime overflow checks whenever overflow cannot be proven impossible. It should eliminate redundant checks whenever it can prove that overflow cannot occur, without changing the program's observable behavior.

22Q: Which numeric types should the initial version of the language support?
22A: The initial version should support fixed-width signed and unsigned integers of 8, 16, 32, and 64 bits, as well as 32-bit and 64-bit floating-point types. Decimal arithmetic may be considered in the future.

23Q: How should floating-point overflow and exceptional values be handled?
23A: The language should support standard IEEE 754 floating-point behavior, including infinities and NaN, as well as an explicit strict mode that detects floating-point exceptional conditions and reports them as errors.

24Q: How should floating-point numbers be compared?
24A: Floating-point numbers should use standard exact comparison semantics by default. Approximate comparison must be explicit and allow the programmer to specify the acceptable tolerance.

25Q: How should the language handle strings?
25A: The language should support convenient UTF-8 strings with automatic memory management, as well as low-level string buffers and views that provide explicit control over memory and lifetimes. The compiler must enforce memory safety rules for both levels.

26Q: How should the language support arrays?
26A: The language should support both fixed-size arrays and dynamic arrays. Fixed-size arrays provide predictable storage, while dynamic arrays allow their size to change at runtime. Memory safety and ownership rules must apply to both.

27Q: What should happen when accessing an array with an invalid index?
27A: Array bounds must be checked by default. If an index is out of bounds, the operation must report an explicit error. Bounds checks may be disabled explicitly in unsafe code, where the programmer is responsible for ensuring that every index is valid.

28Q: How should dynamic arrays handle capacity growth?
28A: The language should support both automatic and explicit capacity management. Dynamic arrays may grow automatically for convenience, while programmers must also be able to explicitly reserve, allocate, and manage capacity for predictable memory usage and maximum performance.

29Q: How should the compiler handle references to elements of dynamic arrays when the array is resized or its memory is relocated?
29A: The compiler must track reference lifetimes and reject the use of references that become invalid after operations that may relocate or resize the array. Array relocation is allowed whenever memory safety rules are satisfied.

30Q: How should arrays be passed to functions by default?
30A: Arrays must be passed by reference without copying their contents by default. The caller retains ownership and controls the array's lifetime. Copying must always be explicit. The compiler must enforce memory safety, reference lifetimes, and access rules.

31Q: How should the language support structured data types?
31A: The language must provide statically typed structures with a fixed set of declared fields and explicit field types. Dynamic objects with fields determined at runtime must be supported through a separate mechanism for cases where the structure is not known in advance.

32Q: How should structures be passed to functions?
32A: Arrays and structures must be passed by reference without copying their contents by default. The caller retains ownership and controls the object's lifetime. Copying must always be explicit. The compiler must enforce memory safety, reference lifetimes, and access rules.

33Q: Should the language support generic types and functions?
33A: Yes. The compiler must specialize generic code for concrete types, generating optimized machine code for each required specialization.

34Q: How should generic functions specify the requirements for their type parameters?
34A: Generic functions must declare explicit constraints specifying the operations or properties required from their type parameters. The compiler must verify that concrete types satisfy these constraints at compile time.

35Q: How should the language support methods on structures?
35A: The language must support both methods declared within structures and standalone functions that operate on structures.

36Q: How should methods declare their access to structure data?
36A: Each method must explicitly declare whether it has read-only access to a structure or is allowed to modify it. The compiler must enforce the declared access restrictions and reject violations.

37Q: How should the language support enumerations?
37A: The language must support both simple enumerations with fixed named values and tagged unions whose variants can contain explicitly typed data. The compiler must ensure that values conform to the declared variants and their associated data types.

38Q: How should the compiler handle incomplete enumeration and tagged union variant matching?
38A: The compiler must require exhaustive handling of all possible variants by default. An explicit fallback branch may be used to handle all remaining variants. The compiler must reject incomplete matching when no fallback branch is provided.

39Q: How should the language organize code into modules?
39A: The language must provide an explicit module system. Each module must explicitly import the modules it depends on, and declaration visibility must be governed by defined access rules.

40Q: How should declaration visibility (functions, structures, and variables) work across modules?
40A: The language must provide two visibility levels: public declarations, which are accessible from other modules, and private declarations, which are accessible only within the current module.

41Q: How should cyclic module imports be handled?
41A: Cyclic module imports must be prohibited. The module dependency graph must be a directed acyclic graph.

42Q: How should compile-time constants work?
42A: Constants may be evaluated at compile time using expressions and functions explicitly permitted for compile-time evaluation.

43Q: Should type sizes and alignments be available at compile time?
43A: The sizes and alignments of all types must be available at compile time and usable in constant expressions.

44Q: Should programmers be able to explicitly control data alignment in memory?
44A: Programmers must be able to specify the memory alignment of types and structure fields, provided that the requested alignment is valid for the target platform.

45Q: Should the language support explicit byte order control for numeric data?
45A: Programmers must be able to explicitly specify byte order when reading and writing data, particularly when working with network protocols and binary formats. Ordinary numeric types must remain independent of the platform's native byte order.

46Q: How should the language support bit manipulation and bit fields?
46A: The language must provide standard bitwise operations (AND, OR, XOR, NOT, and shifts), as well as built-in operations for extracting, setting, and checking individual bits and ranges of bits.

47Q: How should the language support function pointers, first-class functions, and closures?
47A: Functions must be first-class values that can be stored in variables, passed as arguments, and returned from other functions. The language must also support function pointers for low-level programming and closures that can capture variables from their surrounding scope. The compiler must enforce memory safety, ownership, and lifetime rules for captured variables.

48Q: How should variables captured by closures be stored?
48A: Programmers must explicitly choose whether each captured variable is captured by reference or by value. The compiler must enforce the corresponding ownership, memory safety, and lifetime rules.

49Q: Should the language support function overloading based on parameter types?
49A: Yes. Multiple functions may share the same name if their signatures differ in parameter types or parameter counts. The compiler must resolve each function call unambiguously. Function overloading must not depend on return types or implicit type conversions.

50Q: Should the language support variadic functions?
50A: Yes. The language must support variadic functions that accept arguments of different types when their types are known to the compiler. It must also provide a mechanism for low-level C-compatible variadic functions to support interoperability with C libraries.

51Q: Should the language support user-defined operators for custom types?
51A: Yes. Programmers must be able to overload a restricted set of predefined operators for custom types, subject to type safety and unambiguous resolution rules. Programmers must not be able to define arbitrary new operators or change operator precedence and associativity.

52Q: How should comparison and equality work for custom types?
52A: Programmers must explicitly implement comparison and equality operations for custom types when those operations are needed. The compiler must not assume a universal equality or comparison semantics for custom types.

53Q: Should the language support user-defined type conversions?
53A: Yes. Programmers must be able to define explicit conversions between custom types. User-defined conversions must never occur implicitly.

54Q: Should the language support interfaces or traits?
54A: Yes. Types must be able to explicitly implement interfaces or traits that define required operations. The compiler must verify at compile time that each implementing type provides all required operations.

55Q: Should the language support dynamic polymorphism?
55A: Yes. The language must support both static polymorphism through generics and specialization and dynamic polymorphism through interfaces or traits. Programmers must be able to choose the appropriate approach for each use case.

56Q: How should dynamic dispatch be optimized?
56A: The compiler must eliminate dynamic dispatch when the concrete type can be determined at compile time and doing so is beneficial. It must aggressively optimize dynamic dispatch while balancing runtime performance against code size and instruction cache efficiency.

57Q: Should the language support compile-time macros?
57A: Yes. The language must support macros that operate on program structure and generate code at compile time. Generated code must be subject to the language's normal compile-time validation rules.

58Q: How should macros be represented and implemented?
58A: Macros must operate on a structured representation of program code (AST) rather than performing arbitrary text substitution. The compiler must validate the generated code using the language's normal compile-time rules.

59Q: Should the language support runtime reflection?
59A: Yes. The language must provide limited runtime reflection through explicitly requested type metadata retained by the compiler. The compiler must not be required to preserve all program type information in the executable.

60Q: Should the language support annotations for declarations?
60A: Yes. Programmers must be able to attach typed annotations to functions, structures, fields, and other declarations. Annotations must be available to the compiler and development tools and may be included in runtime metadata when explicitly required. Annotations must not execute code automatically.

61Q: How should the language support testing?
61A: The language must provide built-in facilities for declaring and running tests, including result assertions and error reporting. The compiler and development tools must be able to discover and execute tests automatically.

62Q: How should assertions behave in regular code?
62A: Assertions must be available in any code, and programmers must explicitly control which assertions are retained in release builds. Disabling assertions must be an explicit choice.

63Q: How should the language support logging?
63A: The standard library must provide a logging system with configurable log levels, customizable handlers, and the ability to disable unnecessary messages. Logging must not impose mandatory runtime overhead when disabled.

64Q: How should the language support performance profiling?
64A: The language must provide external profiling tool compatibility and built-in facilities for measuring execution time, collecting performance metrics, and analyzing code regions. It must also support collecting runtime execution profiles that the compiler can use to optimize subsequent builds.

65Q: How should the compiler use profiling data?
65A: The compiler must use profiling data to guide optimization decisions, including inlining, specialization, and code layout. Profiling data may influence generated machine code but must not change the program's observable behavior.

66Q: How should the language support building programs from multiple source files?
66A: The compiler must support separate module compilation, reuse of previous compilation results, and incremental recompilation of only the changed modules and their affected dependencies. Whole-program optimizations may be performed during a separate final build stage.

67Q: How should the compiler distribute compiled programs?
67A: The compiler must support generating executable files and static or dynamic libraries, with explicit selection of the target platform.

68Q: How should the build system work?
68A: The language must provide an integrated build system and package manager. It must support a configuration file describing source files, dependencies, build settings, and build targets. The package manager must support downloading dependencies, managing their versions, and building complete projects. The build process must remain predictable and allow explicit control over build settings.

69Q: How should third-party libraries be distributed?
69A: The language must support distributing third-party libraries both as source code and as precompiled artifacts. It must provide a centralized package repository supporting package publication, discovery, downloading, and version management. The package ecosystem must operate independently of C and C++ interoperability.

70Q: How should the compiler ensure build reproducibility?
70A: The build system must produce identical build outputs when given the same source code, dependencies, configuration, and toolchain versions, provided that the explicitly specified target platform and other declared inputs are the same. It must record dependency versions, checksums, and build parameters so that builds can be reliably reproduced later on another machine.

71Q: How should the compiler support different build modes?
71A: The compiler must provide predefined build profiles for development, debugging, and release builds, as well as support fully customizable build profiles. Programmers must be able to explicitly control optimization settings, safety checks, debug information, and other build parameters. Predefined profiles must remain configurable rather than restricting the available compiler capabilities.

72Q: How should the compiler handle compilation errors?
72A: The compiler must detect and report multiple independent errors in a single compilation attempt, providing precise source locations and clear diagnostic messages. It must also provide relevant error context, explain the causes of errors, and suggest fixes when they can be determined with sufficient confidence.

73Q: How should the debugger support the language?
73A: The language must provide its own debugger supporting breakpoints, conditional breakpoints, step-by-step execution, variable inspection, call stack inspection, expression evaluation while execution is paused, and type-aware memory inspection. The compiler must generate the debugging information required by these capabilities. The language must also support integration with external debugging tools.

74Q: How should performance profiling integrate with the debugger?
74A: The debugging and development toolchain must integrate performance profiling for CPU execution, memory allocations, thread activity, and performance bottlenecks. Profiling results must be traceable to the corresponding source code, allowing developers to investigate performance issues directly from the profiling data.

75Q: How should the language support date and time operations?
75A: The standard library must provide types and operations for representing dates, times, time durations, and measuring elapsed time.

76Q: How should the language support filesystem operations?
76A: The standard library must provide a comprehensive filesystem API supporting file and directory reading, writing, creation, deletion, renaming, metadata retrieval, and directory traversal. The language must remain suitable for low-level systems programming, allowing developers to implement custom filesystems and operating system filesystem support independently of the standard library.

77Q: How should the language support low-level memory management and operating system development?
77A: The language must support explicit memory allocation and deallocation, pointer manipulation, and direct memory access in unsafe code. It must also support freestanding compilation without requiring the standard library or a system runtime, enabling developers to use the language for operating system kernels, bootloaders, and other low-level system software.

78Q: How should the language support hardware-specific processor instructions?
78A: The language must support ordinary operations that the compiler translates into machine instructions, built-in hardware instructions for low-level processor control, atomic operations and special system instructions, as well as explicit control over SIMD instructions, processor registers, and architecture-specific instructions. Architecture-specific operations must be explicitly tied to the target architecture, allowing the compiler to verify their availability and validity.

79Q: How should the language support assembly code?
79A: The language must support inline assembly with explicitly declared input and output operands, standalone assembly blocks, and functions implemented entirely in assembly. Assembly code must explicitly specify its target architecture and operate within the unsafe model where required.

80Q: How should the language support interaction with operating systems?
80A: The language must provide a standard library with high-level operating system APIs, direct access to system calls with explicit argument passing and result handling, and the ability to implement custom system call mechanisms and kernel interactions without depending on an existing operating system.

81Q: How should the language support memory management at the operating system level?
81A: The language must support standard allocators, explicit memory allocation and deallocation, custom allocators selectable for individual data structures and code regions, and specialized memory management capabilities for physical memory, virtual memory, memory-mapped devices, and memory pages. Platform-specific memory operations must be governed by target-platform constraints and the language's low-level safety rules.

82Q: How should the language support processor interrupts?
82A: The language must provide dedicated attributes and rules for declaring interrupt handlers, including restrictions on their signatures and behavior. It must also provide facilities for configuring interrupt descriptor tables, controlling interrupt masks, and handling hardware exceptions at the target-architecture level. The compiler must verify architecture-specific requirements wherever possible and explicitly identify responsibilities that depend on the hardware or execution environment.

83Q: How should the language support hardware device interaction?
83A: The language must support operating system APIs and drivers, direct access to I/O ports, device registers, and memory-mapped hardware, as well as dedicated facilities for describing device registers, bit fields, constrained read and write operations, and hardware memory barriers. Hardware access operations must preserve their required semantics, preventing the compiler from removing necessary reads or writes or reordering them in ways that violate device requirements.

84Q: How should the language support control over processor operation ordering?
84A: The language must provide explicit control over memory ordering and synchronization between threads, including different memory ordering guarantees for atomic operations. It must also provide explicit compiler and processor barriers to control operation reordering when interacting with hardware and implementing system-level code. The semantics of each mechanism must be precisely defined so that operation ordering remains predictable.

