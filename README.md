# Ultimate Go Programming, Second Edition

<details>
<summary>001: Design Guidelines</summary>

# Mental Model for Backend Developer
## 1. Integrity
- Read/Write to Memory (Micro-level)
- Data transformation (Macro-level)
- Less code (No getters & setters)
- Error handling (Prevent critical failures)
## 2. Readability
- Don't hide the code
- - Ex: C++'s constructors, destructor features => Difficult to understand "Behavior & Cost" of code
## 3. Simplicity
- Encapsulation (Hiding complexity)

</details>


<details>
<summary>002: Language Syntax</summary>

# 1. Type is LIFE!
- 0001010 can be 10, some color, or other things depending on the TYPE!
- Most PC => AMD64 => 64 bits Architecture => 8 bytes Address Size
- Playground  => AMD64p32 => 32 bits Architecture => 4 bytes Address Size

# 2. Variables
- int: 0
- String: Pointer, Byte (nil, 0)
- Use "short variable declaration operator" for declaration & iniitialization at the same time
- "Conversion" instead of Casting for GO
## Casting
- EX: In fast data transfer, copying bytes can corrupt the memory
## Conversion
- EX: Convert to new bytes (to new memory)

# 3. Struct Type
## Alignment & Padding
### Alignment Concept (Hardware's Memory)
- - Memory Boundary
- - All values should fall inside the boundary
- - Address always falls on a multiple of its own byte size
### Padding Byte for Alignment (Unused byte)
- Counter has to placed within a 2 byte
- Order Fields from LARGEST TO SMALLEST to reduce padding
- See [1] for learn more about "Structure Padding"

## Literal Struct with Anonymous Type
- EX: RESTful API Processing

## Implicit Conversion
- BILL = ALICE
- b = a (Named Type = Named Type) => Not good
- - Implicit Conversion causes the problem
- You need to show your intention (Explicitly)

## Explicit Conversion
- b = bill(a) => Show Conversion Syntax for Go Compiler!

## Named Type = Literal Type
- Bill = e2 is ok
- EX: RESTful API

# 4. Pointers
## Single Threaded
### Definition
- C = Core that controls OS Scheduler
- M = Thread schduled by OS Scheduler (OS level Host, ~2MB Stack)
- P = Logical Processor
- G = Goroutine, Similar to M (Execution, ~2KB Stack)
- Let's focus on Goroutine's Stack

## Pass by Value (Copy)
- Goroutine executes the code
- Execute code inside Isolated Frame (Sandbox)
- Memory Mutation in isolated space (Safe)
- Inefficient

## Pass by Pointer (Sharing Data)
- Warning: Pass by reference is also pass by value (Don't confuse)
- Pointer => Literal Type => Pass across the program boundary
- Memory Mutation outside of iolated space (Requires more care!)
- Efficient

## Escape Analysis for pointer
- Construction happens on the Heap to avoid memory corruption
- GC has to manage heap (Allocation Cost)
- Readability: Never use pointer semantics during construction unless you are returning constructor
- go build -gcflags "-m -m"

## Stack Growth (2KB)
- If you exceed 2KB, value moves from stack to new stack

## Garbage Collection
- We need to reduce latency from GC
- Pacing Algorithm to balance things in GO
- 1. Latency less than 100ms
- - GOGC default: 100%
- 2. GC takes up less than 25% of your CPU Capacity
- Reduce allocation with Pacing Algorithm

## Constants
- Constant only exists at compile time
- - Untyped Constant (Kind) => Can be implicitly converted by compiler, flexibility
- - Typed Constant
- Kind Promotion => EX: 1 + 2.22 = possible, int is promoted to float
- Promote from Kind to Type

## iota & Constants
- Logging

</details>


# Resources
- [0] [Ultimate Go Programming](https://learning.oreilly.com/videos/ultimate-go-programming/9780135261651/)
- [1] [Structure Padding in C](https://youtu.be/aROgtACPjjg)