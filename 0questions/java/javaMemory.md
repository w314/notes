java, memory, stack, heap

# Java Memory

- Java provides automatic memory management.
- JVM divides memory into stack and heap memory.


## `Stack`

- area in memory
- keeps track of the currently executing methods
- stores any variables that these methods create and use
- smaller than heap
- `Stack` Memory in Java is used for:
  - static memory allocation
  - the execution of a thread.
  - it contains:
    - primitive values that are specific to a method
    - references to objects referred from the method that are in a heap.
- LIFO : Access to this memory is in Last-In-First-Out (LIFO) order.
- When the method finishes execution, its corresponding stack frame is flushed, the flow goes back to the calling method, and space becomes available for the next method.
- Variables inside the stack exist only as long as the method that created them is running.
- automatically allocated and deallocated when the method finishes execution. (it grows and shrinks)
- If this memory is full, Java throws `java.lang.StackOverFlowError`.
- Access to this memory is fast when compared to heap memory.
- `threadsafe`, as each thread operates in its own stack.

## `HEAP`

- used for the dynamic memory allocation of Java objects and JRE classes at runtime.

### String Pool

- special area in Heap to store String objects
- a String is stored in Sting Pool if object was created using **literal notation** (`String str = "abd";`)
- a String is stored outside of pool if object was created using **object notation** (`String str = new String("abc");`) EVEN IF object is already in the pool

## `Stack` vs `Heap`

- static vs dynamic memory allocation
- fast vs. slow memory access
- `java.lang.StackOverFlowError` vs `java.lang.OutOfMemoryError`
- automatic memory flush vs garbage collection
- threadsafe vs not threadsafe

<table>
<thead>
<tr>
<td><strong>Parameter</strong></td>
<td><strong>Stack Memory</strong></td>	<td><strong>Heap Space</strong></td></tr>
</thead>
<tbody>
<tr>
<td><strong>Application</strong></td>
<td>Stack is used in parts, one at a time during execution of a thread</td>
<td>The entire application uses Heap space during runtime</td>
</tr>
<tr>
<td><strong>Size</strong></td>
<td>Stack has size limits depending upon OS, and is usually smaller than Heap</td>
<td>There is no size limit on Heap</td>
</tr>
<tr>
<td><strong>Storage</strong></td>
<td>Stores only primitive variables and references to objects that are created in Heap Space</td>
<td>All the newly created objects are stored here</td>
</tr>
<tr>
<td><strong>Order</strong></td>
<td>It's accessed using Last-in First-out (LIFO) memory allocation system</td>
<td>This memory is accessed via complex memory management techniques that include Young Generation, Old or Tenured Generation, and Permanent Generation.</td>
</tr>
<tr>
<td><strong>Life</strong></td>
<td>Stack memory only exists as long as the current method is running</td>
<td>Heap space exists as long as the application runs</td>
</tr>
<tr>
<td><strong>Efficiency</strong></td>
<td>Much faster to allocate when compared to heap</td>
<td>Slower to allocate when compared to stack</td>
</tr>
<tr>
<td><strong>Allocation/Deallocation</strong></td>
<td>This Memory is automatically allocated and deallocated when a method is called and returned, respectively</td>
<td>Heap space is allocated when new objects are created and deallocated by Garbage Collector when they're no longer referenced</td>
</tr>
</tbody>

</table>


## Java Memory Questions
- Describe the difference between the stack and the heap.
