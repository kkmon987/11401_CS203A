# Data Structure – Stack (Theory Notes)

This repository provides a comprehensive, theory-oriented overview of the **Stack** data structure.
The content focuses on **conceptual understanding** only (no programming implementation, no code).

---

## Table of Contents

1. [Definition of Stack](#1-definition-of-stack)  
2. [Core Concepts of Stacks](#2-core-concepts-of-stacks)  
   - [LIFO Principle](#lifo-principle)  
   - [Push and Pop Operations](#push-and-pop-operations)  
3. [Real-World Analogies](#3-real-world-analogies)  
4. [Internal Structure and Memory Model](#4-internal-structure-and-memory-model)  
5. [Types of Stacks](#5-types-of-stacks)  
   - [Bounded (Fixed Size) vs Unbounded (Dynamic) Stacks](#bounded-fixed-size-vs-unbounded-dynamic-stacks)  
   - [Array-based vs Linked-List-based Implementations](#array-based-vs-linked-list-based-implementations)  
6. [Stack Usage in Algorithms](#6-stack-usage-in-algorithms)  
   - [Recursion and Function Calls](#recursion-and-function-calls)  
   - [Parsing (Syntax Checking and Expression Conversion)](#parsing-syntax-checking-and-expression-conversion)  
   - [Backtracking](#backtracking)  
7. [Applications of Stacks](#7-applications-of-stacks)  
   - [Expression Evaluation](#expression-evaluation)  
   - [Undo/Redo Operations](#undoredo-operations)  
   - [Browser Navigation History](#browser-navigation-history)  
8. [Common Operations and Complexity](#8-common-operations-and-complexity)  
9. [Advantages of Stacks](#9-advantages-of-stacks)  
10. [Disadvantages of Stacks](#10-disadvantages-of-stacks)  
11. [Comparison with Queues and Other Linear Structures](#11-comparison-with-queues-and-other-linear-structures)  
12. [Edge Cases and Pitfalls](#12-edge-cases-and-pitfalls)
13. [References](#13-references)  

---

## 1. Definition of Stack

A **stack** is a linear data structure (abstract data type) that stores elements in a sequence where
**both insertion and removal occur at the same end**, called the **top**.

Stacks follow the **Last In, First Out (LIFO)** principle:
the **most recently inserted** element is the **first** to be removed.

Key terms:
- **Top**: the end of the stack where operations occur
- **Push**: insert an element onto the top
- **Pop**: remove and return the top element
- **Peek/Top**: return the top element without removing it
- **Underflow**: popping from an empty stack
- **Overflow**: pushing onto a full bounded stack

---

## 2. Core Concepts of Stacks
<p align="center">
  <img src="assets/images/stack_lifo.png" width="500">
</p>
<p align="center">
  <em>Figure 1. Stack structure illustrating LIFO behavior.</em>
</p>

### LIFO Principle

**LIFO (Last In, First Out)** means the order of removal is the reverse of insertion.
If elements are inserted in the order `A, B, C`, then removal happens as `C, B, A`.

This constrained access pattern is central to why stacks are useful in:
- reversing processes
- undoing actions
- managing nested structures
- backtracking in search

### Push and Pop Operations

<p align="center">
  <img src="assets/images/stack_push_pop.png" width="500">
</p>
<p align="center">
  <em>Figure 2. Push and pop operations on a stack.</em>
</p>

- **Push** adds a new element to the top of the stack and increases stack size by one.
- **Pop** removes the element at the top and decreases stack size by one.
- **Peek/Top** reads the top element without changing the stack.

A correct stack design must define behavior for:
- popping from an empty stack (**underflow**)
- pushing onto a full fixed-capacity stack (**overflow**, only for bounded stacks)

---

## 3. Real-World Analogies

A stack behaves like a **physical stack of plates**:
- you place plates on the top
- you remove plates from the top
- you cannot remove a plate from the middle without removing the plates above it

Other analogies:
- a stack of books on a desk
- a pile of papers (latest on top)
- undo history (latest action undone first)

---

## 4. Internal Structure and Memory Model

A stack is defined by its **behavior (LIFO)**, not by how it is stored in memory.
Internally, stacks are commonly backed by:

- **Contiguous memory (array-like storage)**  
  A stack is stored in a contiguous block of memory with a **top index/pointer** tracking the current top.
  Growth can be fixed (bounded) or adjustable (dynamic resizing).

- **Non-contiguous memory (linked structure)**  
  Each element is stored in a separately allocated node, and the stack maintains a reference to the top node.

Memory implications:
- Array-based stacks often have better **cache locality** (contiguous memory).
- Linked stacks avoid fixed capacity limits but have **pointer overhead** per element.
- System call stacks (function calls) are a real-world example of stack behavior used by runtime execution.
<p align="center">
  <img src="assets/images/stack_array_vs_linked.png" width="650">
</p>
<p align="center">
  <em>Figure 3. Comparison of array-based and linked-list-based stack memory models.</em>
</p>
---

## 5. Types of Stacks

### Bounded (Fixed Size) vs Unbounded (Dynamic) Stacks

**Bounded (Fixed Size) stacks**
- have a predetermined maximum capacity
- pushing beyond capacity causes **overflow**
- simple and efficient when max size is known

**Unbounded (Dynamic) stacks**
- can grow as needed (limited by system memory)
- avoid overflow in normal use
- may require dynamic allocation or resizing strategies

### Array-based vs Linked-List-based Implementations

**Array-based**
- elements stored contiguously
- typically uses an index/pointer to the top
- may be fixed-size or dynamically resized
- strong locality, minimal per-element overhead

**Linked-list-based**
- elements stored in nodes scattered in memory
- top references the most recent node
- natural unbounded growth (until memory runs out)
- extra pointer overhead and allocation/deallocation costs

Note: This repository does not include code; these are conceptual models to explain trade-offs.

---

## 6. Stack Usage in Algorithms

### Recursion and Function Calls

Recursive procedures rely on an implicit **call stack**:
each function call pushes a new frame (context), and returning pops it.
This ensures the most recent call completes first, matching LIFO.

Practical implication:
- deep recursion can cause **stack overflow** (in the call stack sense).

### Parsing (Syntax Checking and Expression Conversion)

Stacks are fundamental in parsing tasks, especially for **nested structures**:
- matching parentheses/brackets/braces
- converting infix expressions to postfix/prefix
- evaluating postfix expressions using operand stacks

The key logic is “last opened must be first closed.”

### Backtracking

Backtracking explores options and reverses the most recent decision first.
A stack naturally records the decision path:
- push a decision/state when moving forward
- pop when encountering a dead end and revert to a previous state

Depth-First Search (DFS) is a classic example that can be expressed with a stack.

---

## 7. Applications of Stacks

### Expression Evaluation

Stacks are used to evaluate expressions efficiently (especially postfix evaluation)
and to manage operators during infix-to-postfix conversion.

### Undo/Redo Operations

Many applications implement:
- **Undo stack**: push each action; undo pops the most recent action
- **Redo stack**: actions undone can be pushed here and reapplied later

This design matches user expectations for reversible histories.

### Browser Navigation History

Browser “Back/Forward” behavior is often modeled with stacks:
- back stack records navigation history
- forward stack records pages you can return to after going back
<p align="center">
  <img src="assets/images/stack_applications.png" width="650">
</p>
<p align="center">
  <em>Figure 5. Real-world applications of stacks.</em>
</p>
---

## 8. Common Operations and Complexity

Let `n` be the number of elements in the stack.

Typical operations:
- **Push**: O(1)
- **Pop**: O(1)
- **Peek/Top**: O(1)
- **isEmpty / size**: O(1)

Space complexity:
- **O(n)** for storing `n` elements
- plus overhead depending on representation (e.g., pointer overhead in linked stacks)

Note:
- If a dynamic array resizes, individual pushes may occasionally cost more,
  but average performance remains efficient over many operations.

---

## 9. Advantages of Stacks

- Simple, minimal interface
- Efficient O(1) push/pop/peek
- Naturally models reversing and nested processes
- Useful for recursion-like workflows, parsing, and backtracking
- Clear intent: “only the most recent item is accessible”

---

## 10. Disadvantages of Stacks

- No random access (cannot efficiently access elements deep in the stack)
- Searching or inspecting deep elements typically requires popping multiple items
- Fixed-size stacks can overflow if capacity is exceeded
- Linked implementations have per-node pointer overhead and less locality
- Traversal without mutation is not part of the core stack abstraction

---

## 11. Comparison with Queues and Other Linear Structures

**Stack vs Queue**
- Stack: **LIFO** (last in, first out)
- Queue: **FIFO** (first in, first out)

Use stacks when you want:
- reverse-order processing
- nested structure handling
- “most recent first” history behavior

Use queues when you want:
- fair, arrival-order processing
- scheduling and buffering
- breadth-first strategies

Stacks can be seen as a restricted case of more general structures (like deques or lists),
optimized for LIFO access.

---

## 12. Edge Cases and Pitfalls

Common issues to guard against in conceptual design and reasoning:

- **Underflow**: popping/peeking from an empty stack
- **Overflow**: pushing into a full bounded stack
- **Unintended destruction**: iterating by popping empties the stack
- **Wrong structure choice**: using a stack when FIFO behavior is required
- **Call stack limits**: recursion depth may exceed system stack capacity

Best practice conceptually:
always define stopping conditions and boundary behavior clearly.

---

## 13. References

1. Wikipedia – Stack (Abstract Data Type)  
   https://en.wikipedia.org/wiki/Stack_(abstract_data_type)

2. Wikipedia – Call Stack  
   https://en.wikipedia.org/wiki/Call_stack

3. GeeksforGeeks – Stack Data Structure  
   https://www.geeksforgeeks.org/stack-data-structure/

4. GeeksforGeeks – Applications, Advantages and Disadvantages of Stack  
   https://www.geeksforgeeks.org/dsa/applications-advantages-and-disadvantages-of-stack/

5. TutorialsPoint – Data Structures: Stack  
   https://www.tutorialspoint.com/data_structures_algorithms/stack_algorithm.htm

6. Simplilearn – Stacks in Data Structures  
   https://www.simplilearn.com/tutorials/data-structure-tutorial/stacks-in-data-structures

7. Acceldata – Stack Data Structure Explained (LIFO Concept)  
   https://www.acceldata.io/blog/stack-data-structure-explained-how-lifo-drives-modern-computing

8. CipherSchools – Understanding Stack in Data Structures  
   https://www.cipherschools.com/blogs/others/understanding-stack-in-data-structures-a-comprehensive-guide/

9. ScrappedScript – Comparing Data Structures: Stack vs Queue  
   https://scrappedscript.com/comparing-data-structures-stacks-vs-queues

10. Programiz – Stack Data Structure  
    https://www.programiz.com/dsa/stack

11. JavaTpoint – Stack Data Structure  
    https://www.javatpoint.com/data-structure-stack

12. StudyTonight – Stack Data Structure  
    https://www.studytonight.com/data-structures/stack-data-structure

