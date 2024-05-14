
# Collection API
>Java Collection API is a set of interfaces and classes to represent a group of objects as a single unit.

A `collection` is a single object which acts as a container for other objects.


### Main Interfaces

`Collection Interface`
- the root interface in the collection hierarchy
- defines common methods like 
    - add()
    - remove() 
    - contains() 
    - size()
    - iterator()

`Set Interface` 
- extends the Collection interface 
- unordered collection of objects
- duplicate values cannot be stored

`List Interface`
- extends the Collection interface
- ordered collection
- can contain duplicate elements
- you can access elements by their index in the list

`Queue Interface`
- extends the Collection interface
- designed for holding elements prior to processing - - provides various methods for managing the queue elements
    - peek() - retreives but does not remove head of the queue
    - poll() - retrieves and removes head of queue

- `Deque Interface`
- extends the Queue interface
- supports element insertion and removal at both ends

`Map Interface`
- does NOT extend the Collection interface 
- but is part of the Collections Framework
- an object that maps keys to values
- cannot contain duplicate keys

- `Iterable`: requires that subtypes must be iterable so it can be traversed using a for-each loop
- `Collection`: defines common behavior that all subtypes should have (add, remove, contains, etc)
- `Set`: defines set-specific behaviors
- `List`: defines list-specific behaviors
- `Queue`: defines queue-specific behaviors
- `Deque`: extends `Queue` supports double-ended queue
- `Map`: does not implement the Collection or Iterable interfaces, but is part of the collection framework.







---- OLD NOTES----

#### List Operations (Methods)

> What are some operations you can perform on a List?

- positional access operations
- search operations
- iteration operations
- range-view operations


### Important Static Methods

- `Collections.sort(myList)`
- `Collections.reverse(myList)`
##### Other Methods

- `isEmpty()`
- `size()`

##### 1. Positional access operations

Manipulates elements based on their numerical position in the list

- `.get()` - using index
- `.set()`
- `.add()` - value OR value at index
- `.addAll()`
- `.remove()` - using index OR value

##### 2. Search operations

Searches for a specified object in the list and returns its numerical position.

- `.indexOf()`
- `.lastIndexOf()`
- `.indexOfSubList()`

##### 3. Iteration operations

`ListIterator`, which allows you to traverse the list in either direction, modify the list during iteration, and obtain the current position of the iterator.

###### Itearation Methods

Inherited from `Iterator`

- `.hasNext()`
- `.next()` - moves cursor forward
- `.remove()`

Added methods:

- `.hasPrevious()`
- `.previous()` - moves cursor backward

```java
// iterating backwards through a  List
for (ListIterator<Type> it = list.listIterator(list.size()); it.hasPrevious(); ) {
    Type t = it.previous();
    ...
}
```

##### listIterator

The List interface has two forms of the listIterator method.

- no arguments: returns a ListIterator positioned at the beginning of the list
- with an int argument: returns a ListIterator positioned at the specified index.

The index refers to the element that would be returned by an initial call to next. An initial call to previous would return the element whose index was index-1. In a list of length n, there are n+1 valid values for index, from 0 to n, inclusive.

###### Cursor

- Intuitively speaking, the `cursor` is always between two elements — the one that would be returned by a call to previous and the one that would be returned by a call to next
- Calls to next and previous can be intermixed, but you have to be a bit careful. The first call to previous returns the same element as the last call to next. Similarly, the first call to next after a sequence of calls to previous returns the same element as the last call to previous.

##### 4. Range-view operations

Returns a List view of the portion of this list whose indices range from fromIndex, inclusive, to toIndex, exclusive.

The returned List is backed up by the List on which subList was called, so changes in the former are reflected in the latter.

- `.sublist(int fromIndex, int toIndex)`

### Queue Interface

- FIFO: add to end/tail, remove from beginning/head
- Java has an interface that represents this data structure
- operations unique to queues:
  - `.offer()` - Inserts a new element onto the Queue
  - `.peek()` - Inspects the element at the front of the Queue, without removing it
  - `.poll()` - Removes an element from the front of the Queue
- using add(), remove(), and element() would throw exceptions

#### Queue implementations

- `LinkedList`
- `ArrayDeque`
  - resizable array implementation of `Deque`interface
- `PriorityQueue`
  - elements are ordered by priority based on their natural ordering (or a Comparator)
- `ArrayBlockingQueue`
  - array-backed
  - implements `BlockingQueue` interface
  - supports operations that wait on the queue to contain an element or for space to become available in the queue
  - Solution to the producer-consumer problem, where a producer thread inputs elements into the array while a consumer thread removes them for processing

### Stack Interface - LEGACY USE Deque INSTEAD

- LIFO: add to end/top, remove from end/top
- Java has a legacy class that represents this data structure
- Java recommends the Deque type instead
- stack operations:
  - `push`: add to top
  - `peek`: view top
  - `pop`: remove top

### Deque Interface

- Extends the Queue interface
- Short for “double-ended queue", pronounced “deck”
- Supports element insertion and removal from both ends of the queue
- Can be used to implement a stack, with Last-In-First-Out (LIFO) behavior

#### Deque Methods

This interface defines methods to access the elements at both ends of the deque.

Each of these methods exists in two forms:

- one throws an exception if the operation fails,
- the other returns a special value (either null or false, depending on the operation).

(The latter form of the insert operation is designed specifically for use with capacity-restricted Deque implementations; in most implementations, insert operations cannot fail.)

<table>
<thead>
<tr>
<td></td>
<td>First Element (Head)	</td>
<td></td>
<td>Last Element (Tail)</td>
</tr>
<td></td>
<td>Throws exception</td>
<td>Special value</td>
<td>Throws exception</td>
<td>Special value</td>
<tr>
</thead>
<tbody>
<tr>
<td>Insert</td>
<td>addFirst(e)</td>
<td>offerFirst(e)</td>
<td>addLast(e)</td>
<td>offerLast(e)</td>
</tr>
<tr>
<td>Remove</td>
<td>removeFirst()</td>	
<td>pollFirst()</td>	
<td>removeLast()</td>	
<td>pollLast()</td>
</tr>
<tr>
<td>Examine</td>	
<td>getFirst()</td>	
<td>peekFirst()</td>	
<td>getLast()</td>	
<td>peekLast()</td>
</tr>
</tbody>
</table>

### Set Interface

- collection that does not contain duplicates
- this interface provides set operations (union, intersection, difference)

#### Set Implementations

- HashSet: insertion order not guaranteed
- LinkedHashSet: maintains insertion order
- TreeSet: elements are sorted

#### Set Methods

- `.addAll()` - UNION adds elements from one set to the other, no duplicates
- `.retainAll()` - INTERSECTION retains only common elements between two sets
- `.removeAll()` - DIFFERENCE removes all elements from first set that are contained in second set

### Map Interface

- each entry in a map is a key-value pair
- specifies two generic type parameters
- keys are unique
- part of the `Collections Framework`
- does NOT implement `Collections interface`
- there are 2 interfaces for implementing `Map` in Java:
  - `Map`
  - `SortedMap`

#### Map Implementations

- `HashMap`
  - does NOT maintain order of insertion
  - fast insertion/retreival
  - permits 1 null key and null values
  - `HashTable`:
    - older, thread safe implementation of `HashMap`
    - does not allow null keys or null values
- `LinkedHashMap`
  - maintains insertion order
- `TreeMap`
  - entries are sorted by keys
  - keys are stored in a Sorted Tree structure
  - slow insertion/retreival
  - cannot contain null keys

#### Map Methods

- `.put()`
- `.get()` - return `null` if not found
- `.remove()`
- `.entrySet()`
- `.keySet()`
- `.values()`

#### Iterating over map

- does NOT implement the `Iterable interface`
- therefore cannot be iterated over directly
- use instead
  - `.entrySet()` method to iterate over `Map.Entry`
  - `.keySet()` method to iterate over keys
  - `.values()` method return a `Collection` that can be iterated over

### Classes of the Collection API

#### ArrayList Class

- implements the `List` interface
- a data structure which contains an array within it
- resizes dynamically - Once it reaches maximum capacity, an ArrayList will increase its size by 50% by copying its elements to a new (internal) array.
- fast traversal: O(1) - because elements can be randomly accessed via index, just like an array
- slow insertion or removal of elements : O(n) - since there is a risk of having to resize the underlying array
- `parameterized type` - declared as using generics
- cannot use primitives, must use their wrapper classes
- better for storing and accessing data

#### LinkedList Class

- implements both the `List` and `Dequeue` interfaces
- the data structure is composed of nodes internally, each with a reference to the previous node and the next node - i.e. a doubly-linked list.
- insertion or removal of elements is fast
- traversal is slow for an arbitrary index
- better for manipulating data (vs. storing and accessing)

##### Linked List Methods

- addFirst()
- addLast()
- getFirst()
- getLast()
- indexOf()
- get() (uses index)
- listIterator()

#### ArrayList vs. LinkedList

- When the rate of addition or removal rate is more than the read scenarios, then use a LinkedList. On the other hand, when the frequency of the read scenarios is more than the addition or removal rate, then ArrayList takes precedence over LinkedList.
- Since the elements of an ArrayList are stored more compact as compared to a LinkedList; therefore, the ArrayList is more cache-friendly as compared to the LinkedList. Thus, chances for the cache miss are less in an ArrayList as compared to a LinkedList. Generally, it is considered that a LinkedList is poor in cache-locality.
- Memory overhead in the LinkedList is more as compared to the ArrayList. It is because, in a LinkedList, we have two extra links (next and previous) as it is required to store the address of the previous and the next nodes, and these links consume extra space. Such links are not present in an ArrayList.
- ArrayList in the multithreading environment does not provide thread safety. This is because ArrayList is not synchronized.


## Collections API Questions
> What is a Collection?


> What is the Collection API?
> Java has the Collection API that implements common data structures