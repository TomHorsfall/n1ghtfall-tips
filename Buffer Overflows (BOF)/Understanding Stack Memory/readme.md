# Understanding Stack and Heap Memory

Resources:
- https://medium.com/young-coder/an-illustrated-guide-to-memory-the-stack-the-heap-and-pointers-40a604f7bc53
- https://www.guru99.com/stack-vs-heap.html#:~:text=The%20heap%20is%20a%20memory,It%20supports%20Dynamic%20memory%20allocation.

 

## Stack

- A temporary storage space
- The name comes from the fact that the information stored here is “stacked” up
- The **oldest data is on the bottom and the newest data is on top**
- Programming languages maintain the stack for you automatically
- The stack is great for speed as it can push items off the stack at a quick pace.
 

## Stack Limitations

There are a few complications/ limitations of Stack memory:

1. The stack is small and there is only so much space. The stack is not meant to be used as a large storage space.
2. Stack memory cannot be expanded. It stays the same when it is created.
3. You can’t selectively remove something in the middle of the stack to get your memory back.
4. To grab a value in the middle of the stack, the computer needs to dig through everything on top first
 

To solve these problems there is what is called **Heap Memory**

 

## Heap Memory

- The heap is a big pool of memory where you can store all the data that doesn’t belong on the stack
- It is called the heap, because like my room, it is a total mess with an unorganized HEAP of clothes on the floor
- Bigger objects belong on the heap
- The heap is also more flexible than the stack wherein it can expand memory to accommodate larger pieces of data
- To better understand the heap here is a view of a function in python:

```python
global_var = "This var is stored in the heap"

def itspython():
    local_var = "This var is stored in stack memory because it is inside a function"
```

 

## Pointers

What is a **pointer**?

- A pointer is a memory address
- So rather than storing a **value** a pointer stores a **memory address**
- The beauty of this is you can place pointers on a stack. This way rather than storing a large piece of information on the stack itself, it can store a reference to the memory stored in heap
 

Understanding this information can help in security for understanding buffer overflows as well as solving coding issues.


## Buffer Overflows Explained

https://www.imperva.com/learn/application-security/buffer-overflow/

## Types of BOF Attacks

**Stack Based Buffer Overflow Attacks**
- More common
- Leverage stack memory (function and local variable data) that only exists during the execution time of a function

**Heap-Based Attacks**
- Harder to carry out
- Involve flooding the memory space allocated for a program beyond memory used for current runtime operations
 

## Commonly Exploited Languages

- C and C++
- These languages do not have built in safeguards against overwriting or accessing data in their memory.
Mac OSx, Windows, and Linux are all written in C and C++
- Languages like PERL, Java, JS, and C# use built-in safety mechanisms that minimize these issues
 

## Preventing Buffer Overflow

**ASLR Address Space Randomization**: Randomly moves around the address space locations of data regions.
BOF attacks need to know the locality of executable code. By randomizing address spaces, this makes finding executable code virtually impossible
**Data Execution Prevention**: Flags certain areas of memory as non-executable or executable which stops an attack form running code in a non-executable region
**Structured Exception Handler Overwrite Protection (SEHOP)** - Helps stop malicious code from attacking Structured Exception Handling, a built-in system for managing hardware and software excptions.
This prevents an attacker from being able to make use of the SEH overwrite exploitation technique.
It does this by overwriting an exception registration record (where the exception data is stored) on a thread’s stack
 

https://www.mandiant.com/resources/six-facts-about-address-space-layout-randomization-on-windows#:~:text=ASLR%20works%20by%20breaking%20assumptions,data%20execution%20prevention%20(DEP).

## ASLR

- One important thing to remember is that learning about the defensive side of BOFs will also help in understanding how BOF attacks work.
- If we know the defenses, we can see why/ how these attacks are SUPPOSED to work, and what defenders and developers are doing to stop them.
- Address Space Layout Randomization essentially randomizes the address space of an individual computer
- Previous to this, Microsoft would store certain files in the exact same locations across all OSes. This was a grave mistake because this means if 10 computers on a network had a vuilnerable OS installed, someone could write a worm that propagates across all ten machines because the attacker knows that all of those machines have the same memory setup.
 
 

## Return Oriented Programming (ROP) Attacks

https://resources.infosecinstitute.com/topic/return-oriented-programming-rop-attacks/

 