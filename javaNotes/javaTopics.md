## JSON

_ignore implementation, the second part of it is in JavaScript_

- `JSON` (`JavaScript Object Notation`) is a lightweight data-interchange format.
- JSON Object is a set of key and value pair enclosed within curly braces
- a key is a string enclosed in quotation marks
- a value can be a:
  - string
  - number
  - boolean expression
  - array, or object
- `parse()` is a commonly used method or function name used to read JSON strings in a variety of programming
  languages.

JSON object syntax:

```javascript
let Book = {
  id: 110,
  language: "Python",
  author: ["John", "Ben"],
};
```

Applications of JSON:

- transmit data between the server and web application
- helps transmit and serialize all types of structured data
- allows us to perform asynchronous data calls without the need to do a page refresh
- Web services and Restful APIs use the JSON format to get public data.

## REST

_You will not be assessed over the example in the Implementation section (we will not cover Servlets)_

DEFINITION:

> Representational State Transfer (REST) is an architectural style that defines a set of constraints to be used for creating web services.

- Representational State Transfer
- architecture for exposing information and functionality between software or devices
- used to fetch or give some information from a web service
- information provided is a representation of the state of a given resource
- representation is usually JSON
- all communication done via REST API uses only HTTP requests
- In HTTP there are five methods that are commonly used in a REST-based Architecture: POST, GET, PUT, PATCH, and DELETE. These correspond to create, read, update, and delete (or CRUD) operations respectively.

`REST` vs.<br>
`SOAP` (`Simple Access Protocol`) and <br>
`RPC` (`Remote Procedure Call`)

- REST uses less bandwidth than SOAP
- SOAP can only return `xml`, REST can return json, xml, yaml and more
- in REST users are not required to know procedure names or spedific parameters in a specific order like in RPC

### Is RESTful API right for the application

There are some key `constraints` to think about when considering whether a RESTful API is the right type of API for your needs:

- `Client-Server`: This constraint operates on the concept that the client and the server should be separate from each other and allowed to evolve individually.
- `Stateless`: REST APIs are stateless, meaning that calls can be made independently of one another, and each call contains all of the data necessary to complete itself successfully.
- `Cache`: Because a stateless API can increase request overhead by handling large loads of incoming and outbound calls, a REST API should be designed to encourage the storage of cacheable data.
- `Uniform Interface`: The key to the decoupling client from server is having a uniform interface that allows independent evolution of the application without having the application’s services, or models and actions, tightly coupled to the API layer itself.
- `Layered System`: REST APIs have different layers of their architecture working together to build a hierarchy that helps create a more scalable and modular application.
- `Code on Demand`: Code on Demand allows for code or applets to be transmitted via the API for use within the application.

### REST resources and url construction

#### REST Resource

- entity or data that API can provide info about
- can be identified by a URL
- can allow actions to be performed on it (GET, POST, PUT, DELETE)

Singleton and Collection Resources
A resource can be a singleton or a collection.

For example, “customers” is a collection resource and “customer” is a singleton resource (in a banking domain).

We can identify “customers” collection resource using the URI “/customers“. We can identify a single “customer” resource using the URI “/customers/{customerId}“.

Collection and Sub-collection Resources
A resource may contain sub-collection resources also.

For example, sub-collection resource “accounts” of a particular “customer” can be identified using the URN “/customers/{customerId}/accounts” (in a banking domain).

Similarly, a singleton resource “account” inside the sub-collection resource “accounts” can be identified as follows: “/customers/{customerId}/accounts/{accountId}“.

### URI

`REST API`s use Uniform Resource Identifiers (`URI`s) to address resources.

The constraint of a uniform interface is partially addressed by the combination of URIs and HTTP verbs and using them in line with the standards and conventions.

# Constraints (principles)

- client/server relationship: separate components interacting through an interface
- uniform interface: use of resources, self-descriptive messages
- stateless: each message contains all info needed
- HATEOS / Hypertext as the engine of application state (make API discoverable in state through links!)
- layered system: application itself is ideally in layers interacting through interfaces
- cachable: responses should specify if info is cachable or not.

### Best Practices

- use nouns for resources (users, posts, etc) not verbs
- use plurals for resources that are collections
- single resources are represented by a name or id
- send appropriate response code back

resource archetypes categories:

- document
- collection
- store
- controller

Put a resource into one archetype and then use its naming convention consistently.

For uniformity’s sake, resist the temptation to design resources that are hybrids of more than one archetype.

#### document

A document resource is a singular concept that is akin to an object instance or database record.

In REST, you can view it as a single resource inside resource collection. A document’s state representation typically includes both fields with values and links to other related resources.

Use “singular” name to denote document resource archetype.

http://api.example.com/device-management/managed-devices/{device-id}
http://api.example.com/user-management/users/{id}
http://api.example.com/user-management/users/admin

#### collection

A collection resource is a server-managed directory of resources.

Clients may propose new resources to be added to a collection. However, it is up to the collection resource to choose to create a new resource or not.

A collection resource chooses what it wants to contain and also decides the URIs of each contained resource.

Use the “plural” name to denote the collection resource archetype.

http://api.example.com/device-management/managed-devices
http://api.example.com/user-management/users
http://api.example.com/user-management/users/{id}/accounts

#### store

A store is a client-managed resource repository. A store resource lets an API client put resources in, get them back out, and decide when to delete them.

A store never generates new URIs. Instead, each stored resource has a URI. The URI was chosen by a client when the resource initially put it into the store.

Use “plural” name to denote store resource archetype.

http://api.example.com/song-management/users/{id}/playlists

#### controller

A controller resource models a procedural concept. Controller resources are like executable functions, with parameters and return values, inputs, and outputs.

Use “verb” to denote controller archetype.

http://api.example.com/cart-management/users/{id}/cart/checkout http://api.example.com/song-management/users/{id}/playlist/play

Consistency is the key
Use consistent resource naming conventions and URI formatting for minimum ambiguity and maximum readability and maintainability. You may implement the below design hints to achieve consistency:

- Use forward slash (/) to indicate hierarchical relationships
  The forward-slash (/) character is used in the path portion of the URI to indicate a hierarchical relationship between resources. e.g.

http://api.example.com/device-management
http://api.example.com/device-management/managed-devices
http://api.example.com/device-management/managed-devices/{id}
http://api.example.com/device-management/managed-devices/{id}/scripts
http://api.example.com/device-management/managed-devices/{id}/scripts/{id}

- Do not use trailing forward slash (/) in URIs
  As the last character within a URI’s path, a forward slash (/) adds no semantic value and may confuse. It’s better to drop it from the URI.

http://api.example.com/device-management/managed-devices/ http://api.example.com/device-management/managed-devices /_This is much better version_/

- Use hyphens (-) to improve the readability of URIs
  To make your URIs easy for people to scan and interpret, use the hyphen (-) character to improve the readability of names in long path segments.

http://api.example.com/device-management/managed-devices/
http://api.example.com/device-management/managed-devices /_This is much better version_/
Do not use underscores ( _ )
It’s possible to use an underscore in place of a hyphen to be used as a separator – But depending on the application’s font, it is possible that the underscore (_) character can either get partially obscured or completely hidden in some browsers or screens.

To avoid this confusion, use hyphens (-) instead of underscores ( \_ ).

http://api.example.com/inventory-management/managed-entities/{id}/install-script-location //More readable

http://api.example.com/inventory-management/managedEntities/{id}/installScriptLocation //Less readable

- Use lowercase letters in URIs

- do not use file extensions

Apart from the above reason, if you want to highlight the media type of API using file extension, then you should rely on the media type, as communicated through the Content-Type header, to determine how to process the body’s content.

http://api.example.com/device-management/managed-devices.xml /_Do not use it_/

http://api.example.com/device-management/managed-devices /_This is correct URI_/

- Use query component to filter URI collection
  Often, you will encounter requirements where you will need a collection of resources sorted, filtered, or limited based on some specific resource attribute.

For this requirement, do not create new APIs – instead, enable sorting, filtering, and pagination capabilities in resource collection API and pass the input parameters as query parameters. e.g.

http://api.example.com/device-management/managed-devices
http://api.example.com/device-management/managed-devices?region=USA
http://api.example.com/device-management/managed-devices?region=USA&brand=XYZ
http://api.example.com/device-management/managed-devices?region=USA&brand=XYZ&sort=installation-date

### Exposing and Consuming RESTful API endpoints

_You will not be assessed over implementation code of steps 3 and 4 (Bennu Framework)_

## Logging

> What is logging and what are the benefits of it?
>
> Logging is keeping a log of events that occur form an application.

### Logback

- `Logback` is one of the most widely used logging frameworks in the Java Community.(It's a replacement for its predecessor, Log4j.)
- Logback offers:
  - faster implementation
  - more options for configuration
  - more flexibility in archiving old log files
  - smaller memory footprint

Resons to prefer `Logback` over `Log4j`:

- small and speedy: components are faster and have a smaller memroy footprint
- much better tested framework
- automatically reloads configuration files
- gracefully recovers from I/O errors (no need to restart app after server fail, just to get logging to work again)
- automatic removel of old log archives
- automatic compression of archived log files

### Logback Architecture

The `Logback architecture` is comprised of three classes:

- `Logger` - object that allows you to create logs
- `Appender` - represents the destination of a log
- `Layout` - controls log message formatting

### How to use a Logger

> How would we configure logging in an application?

1. configure logger
2. use logger objects in classes you want to use logging
3. use the logger object's logging level method

### Logging Levels

> Describe the different logging levels and how they should be used.

- TRACE - most fine-grained information
- DEBUG - should be used for information that may be needed for diagnosing issues and troubleshooting
- INFO - standard log level
- WARN - indicates that something unexpected happened, but the code can continue the work
- ERROR - hould be used when the application hits an issue preventing one or more functionalities from properly functioning

Setting level at a certain level gives all level on and above that level.

What are logging levels good for?

- filtering
- allow you to configure your logging process so that it behaves differently according to each level:
  - Granularity. It might make sense to decrease or increase the granularity of logging according to the level.
  - Target. You might want level X entries to be logged to files, and level Y entries to be logged to a database.
  - Retention policy. This is linked to granularity. If a certain level has a higher granularity, it might make sense to delete the log entries in that level more frequently, for example, to save disk space.

#### Setup & Configuration

- if no configuration is given, default logger can be used
- default logger uses debug logging level
- to configure create `logback.xml` file under `main/resources`
- create appenders
- create loggers and assign them appenders

##### Add dependency to `pom.xml`

`Logback` uses the Simple Logging Facade for Java (`SLF4J`).

`Classpath`
Logback also requires logback-classic.jar on the classpath for runtime.

We'll add this to `pom.xml` as a test dependency:

```xml
<!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.4.11</version>
    <scope>test</scope>
</dependency>
```

##### Add `logback.xml` configuration file

We'll create a text file named `logback.xml` and put it somewhere in our classpath:

```xml
<configuration>
  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder>
      <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
  </appender>

  <root level="debug">
    <appender-ref ref="STDOUT" />
  </root>
</configuration>
```

#### Use Logger

```java
package main;

public class Example {

    // create logger object
    private static final Logger logger = LoggerFactory.getLogger(Example.class);

    // use logging methods
    public static void main(String[] args) {
        logger.info("Example log from {}", Example.class.getSimpleName());
    }
}
```

## Mockito

> What is Mockito and why would we use it?

> What is a mock?

### Mockito

Mocking framework used for unit tests

A mock object is a dummy implementation for an interface or a class.

Mockito records the interaction with mock and allows you to check if the mock object was used correct, e.g. if a certain method has been called on the mock. This allows you to implement behavior testing instead of only testing the result of method calls.

Mockito:

- uses annotations to identify its functionality, similar to JUnit
- `mock`: replacement object - behavior is stubbed unless we request real behavior
- `spy`: replacement object - behavior is real unless we request it is stubbed
- from the docs: "Real spies should be used carefully and occasionally, for example when dealing with legacy code."
- `stub`: replacement behavior

### Creating Mocks

Dependency Injection using @Mock, @InjectMock, and @openMocks

_NOTE: @openMocks is the syntax used in newer versions of Mockito and it replaces @initMocks. Both do the same thing._

- `@InjectMocks` is used on the object being tested to specify what to inject with a mock
- `@Mock` to specify what should be mocked
- `MockitoAnnotations.openMocks()` is used to perform the injection
- Mockito will use any constructors available in the real object for injection, otherwise it will try using setters, and then finally it will try using fields

### Stubbing

- when() is used to target an invocation
- thenReturn() or thenThrow() is used to return dummy results / throw exceptions
- if a mock's method isn't stubbed, it will return default values (null, empty collection, 0, false, etc)
- doThrow(), doAnswer(), doNothing(), doCallRealMethod() are used with void methods (https://www.baeldung.com/mockito-void-methods)

### Verify

- a mock will remember all method invocations on it for verification
- `times(x)` is used to verify a behavior was invoked x many times
- `never()` is used to verify a behavior was not invoked
- `atMostOnce()`, `atLeastOnce()`, `atMost(x)`, `atLeast(x)`

WK7

## Generics

- enables classes to be parameterized so they can be re-used with different types as input, like methods
- alternative is using Object as type of state, which would require casting and could lead to runtime issues
- generics add stability to your code by making more of your bugs detectable at compile time

### creating a class that uses generics

- add a generic type declaration to your class, ex `ClassName<T>`
- you can specify more than one type variable as a parameter
- use the type variables throughout the class
- `bounded types`: requirement that type must be subtype or of same type as specified type
  - ex: `ClassName<T extends SuperType>`
  - supertype can be a class or interface

### using a generic class

- generic type invocation: when using the parameterized class, replace the type param name with the actual type you want to use
- ex: `ArrayList<String> stringList`
- raw type: if you do not specify a type, the Object type will be used

### type parameter naming conventions

Type params are single, uppercase letters.

- E: Element
- K: Key
- N: Number
- T: Generic Data Type
- V: Value
- S,U,V etc: 2nd, 3rd, 4th for multiple generic data types

## Iterators

- objects that allow you to traverse a Collection
- are used "behind the scenes" in enhanced for loops

The `Iterable` interface defines a data structure which can be directly traversed using the `.iterator()` method, which returns an `Iterator`.

- Any class that implements the Iterable interface needs to override the `iterator()` method
- Any class implementing the Iterator interface needs to override the `hasNext()` and `next()` methods provided by the Iterator interface.
- The Iterator instance stores the iteration state. That means it provides utility methods to get the current element, check if the next element exists, and move forward to the next element if present. In other words, an Iterator remembers the current position in a collection and returns the next item in sequence if present. The Iterable, on the other hand, doesn’t maintain any such iteration state
- The contract for Iterable is that it should produce a new instance of an Iterator every time the iterator() method is called. This is because the Iterator instance maintains the iteration state, and things won’t work as if the implementation returns the same Iterator twice.
- For an Iterable, we can move forward only in the forward direction, but some of the Iterator subinterface like ListIterator allows us to move back and forth over a List.
- Also, Iterable doesn’t provide any method to modify its elements, nor can we modify them using the for-each loop. But Iterator allows removing elements from the underlying collection during the iteration with the remove() method.

### Iterator Methods:

- `.hasNext()` - returns true if the iteration has more elements
- `.next()` - returns the next element in the iteration.
- `.remove()` - removes element from underlying collection (can only be called on modifiable Collections!)
- you cannot modify using Collection methods during iteration!

### List Iterator

- additionally has operations that use indexes
- can iterate backwards
- `.nextIndex()`
- `.previousIndex()`
- `.previous()`
- `.hasPrevious()`

### `Iterable`

An Iterable represents a collection that can be traversed.

To traverse an iterable:

#### 1. `Enhanced For Loop`

```java
Set<String> names = new ArrayList<>();

for (String name : names) {
  System.out.println(name);
}
```

### 2. using an `Iterator`

```java
Iterator<Integer> iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

### 3. using `.forEach()`

```java
Iterator<Integer> iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();
iterator.forEachRemaining(System.out::println);
```

### 4. using `lambda`

```java
for (Integer i: (Iterable<Integer>) () -> iterator) {
    System.out.println(i);
}
```

## Collection API

_Assessment: Not PriorityQueue or Vector. Know how to work with Collections and yes, knowing the difference between a linked list and arraylist is useful._

> What is a Collection?

A `collection` is a single object which acts as a container for other objects.

> What is the Collection API?
> Java has the Collection API that implements common data structures

### Important Interfaces

- `Iterable`: requires that subtypes must be iterable so it can be traversed using a for-each loop
- `Collection`: defines common behavior that all subtypes should have (add, remove, contains, etc)
- `Set`: defines set-specific behaviors
- `List`: defines list-specific behaviors
- `Queue`: defines queue-specific behaviors
- `Deque`: extends `Queue` supports double-ended queue
- `Map`: does not implement the Collection or Iterable interfaces, but is part of the collection framework.

## Queue

- FIFO: add to end/tail, remove from beginning/head
- Java has an interface that represents this data structure
- operations unique to queues:
  - `offer`: attempt and adds, if you are able to
  - `peek`: attempt to get head, if there is one
  - `poll`: attempt and remove, if you are able to
- using add(), remove(), and element() would throw exceptions

### Queue implementations

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

## Stack

- LIFO: add to end/top, remove from end/top
- Java has a legacy class that represents this data structure
- Java recommends the Deque type instead
- stack operations:
  - `push`: add to top
  - `peek`: view top
  - `pop`: remove top

## Sets

- collection that does not contain duplicates
- this interface provides set operations (union, intersection, difference)

### Implementations

- HashSet: insertion order not guaranteed
- LinkedHashSet: maintains insertion order
- TreeSet: elements are sorted

### Useful Methods

- addAll() - (union) adds elements from one set to the other, no duplicates
- retainAll() - (intersection) retains only common elements between two sets
- removeAll() - (difference) removes all elements from first set that are contained in second set

## Maps

- each entry in a map is a key-value pair
- specifies two generic type parameters
- keys are unique
- part of the `Collections Framework`
- does NOT implement `Collections interface`
- there are 2 interfaces for implementing `Map` in Java:
  - `Map`
  - `SortedMap`

### Implementations

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

### Useful Methods

- put()
- get()
- remove()
- entrySet()
- keySet()
- values()

### Iterating over map

- does NOT implement the `Iterable interface`
- therefore cannot be iterated over directly
- use instead
  - `.entrySet()` method to iterate over `Map.Entry`
  - `.keySet()` method to iterate over keys
  - `.values()` method return a `Collection` that can be iterated over

## ArrayList Class

- implements the `List` interface
- a data structure which contains an array within it, but can resize dynamically.
- Once it reaches maximum capacity, an ArrayList will increase its size by 50% by copying its elements to a new (internal) array.
- Traversal is fast (constant time) because elements can be randomly accessed via index, just like an array.
- Insertion or removal of elements is slow, however (linear time, since there is a risk of having to resize the underlying array)
- ArrayList is a parameterized type
- cannot use primitives, must use their wrapper classes
- better for storing and accessing data

## LinkedList Class

- implements both the `List` and `Dequeue` interfaces
- the data structure is composed of nodes internally, each with a reference to the previous node and the next node - i.e. a doubly-linked list.
- insertion or removal of elements is fast
- traversal is slow for an arbitrary index
- better for manipulating data (vs. storing and accessing)

### Linked List Methods

- addFirst()
- addLast()
- getFirst()
- getLast()
- indexOf()
- get() (uses index)
- listIterator()

## ArrayList vs. LinkedList

- When the rate of addition or removal rate is more than the read scenarios, then use a LinkedList. On the other hand, when the frequency of the read scenarios is more than the addition or removal rate, then ArrayList takes precedence over LinkedList.
- Since the elements of an ArrayList are stored more compact as compared to a LinkedList; therefore, the ArrayList is more cache-friendly as compared to the LinkedList. Thus, chances for the cache miss are less in an ArrayList as compared to a LinkedList. Generally, it is considered that a LinkedList is poor in cache-locality.
- Memory overhead in the LinkedList is more as compared to the ArrayList. It is because, in a LinkedList, we have two extra links (next and previous) as it is required to store the address of the previous and the next nodes, and these links consume extra space. Such links are not present in an ArrayList.
- ArrayList in the multithreading environment does not provide thread safety. This is because ArrayList is not synchronized.

## common UNIX commands

> What are some common Linux commands? Why are they useful?

```shell
#  list directory content
ls

# change directory
cd

# display current working directory path
pwd

# create directory
mkdir

# create empty file
touch

# echo redirected to file with > will create new file
echo "New file content" > new_file.txt

# view file
cat filename

# create new file
cat > newfile

# copy sourcefile content to destionation file
cat sourcefile > destinationfile

# search string in file
grep mystring myfile

# compare 2 files, output lines that are different
diff file1 file2

# move file1 to directory1
mv file1 directory1
# prompt if we would overwrite a file
mv - i file1 directory1
# do not move if we would overwrite a file
mv -n file1 directory1
# only move if the source file is newer than destination file
mv -u file1 directory1
# create backup of overwritten destination file with same name 1 added to end
mv -b file1 directory1

# rename file1 to file2
mv file1 file2

# copy file1 to file2
cp file1 file2
# flags
# interactive, warn before overwriting
-i
# create backup of destination file
-b
# use force: delete destination file if cannot be opened
-f
# recursive, copy directory with all subdirectories
-r
# preserve characteristics: times of last modification, etc
-p

# delete file
rm file1
# delete directory with all files and subdirectories
rm -r directory1
# force deletion flag
-f



mv
rm

cat
grep
cp
```

## source control management

> What is source control management? Why is it useful?

`Version control` = Revision control = `Source Control Management` (`SCM`), is a process to manage a collection of source code and its changes.

- manage and keep track of all your source code
- all your changes are being stored in a repository.
- there are 2 types of Version Control Systems
  - the Centralized Version Control System (CVCS)
  - Distributed (DVCS).

The concept of `CVCS` is that it works on a Client-Server relationship. The repository is located in one place and provides access to many clients.

On the contrary, in `DVCS`, every user has a local copy of the repository in addition to the central repo on the server-side.

## Git

- you have the entire history of the project right there on your local disk

> What are the main states that your files can reside in when using Git?

Git has three main `states` that your files can reside in:

- `modified` - you have changed the file but have not committed it to your database yet
- `staged` - you have marked a modified file in its current version to go into your next commit snapshot.
- `committed` - the data is safely stored in your local database

> What are the main sections of a Git project?

The three main `sections` of a Git project:

- the `working tree` (or `working directory`, as in the diagram below) is a single checkout of one version of the project, downloaded to your local machine. The working tree is the set of all files and folders a developer can add, edit, rename and delete during application development. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.
- the `staging area` is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the `“index”`, but the phrase “staging area” works just as well. (See diagram below)
- `Git directory`(a.k.a. `repository folder`) is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer
  - stores the history of all changes made to the files in a Git project
  - name of directory: `.git`

Two types of Git repositories, based on user permissions:

- Bare Repositories
  - Software development teams use bare repositories to share changes made by team members.
  - Individual users aren't allowed to modify or create new versions of the repository.
- Non-Bare Repositories

  - With non-bare repositories, users can modify the existing repository and create new versions.
  - By default, the cloning process creates a non-bare repository.

  > What are some common operations you would be performing when using Git?

- Understand how to push to repo
- Understand how to use branches
- Understand how to merge

```shell
# initialize repository
git init

# clone repository
git clone [url] [directory]

# get status of git repository
git status

# stage all files in directory
git add .

# commit changes
git commit -m 'commit message'

# push code to remote repository
git push

# create new branch
git branch new-branch

# move to new branch
git checkout new-branch

# shortcut to create and move to new branch
get checkout -b new-branch

# pull data from remote repository
git pull

# merge branch to master
#  1. move to master first
git checkout master
#  2. merge new branch
git merge new-branch
```

### Git Bash

- Git Bash is an application for Microsoft Windows environments which provides an emulation layer for a Git command line experience. A package that installs Bash, some common bash utilities, and Git on a Windows operating system.
- `Bash` is an acronym for `Bourne Again Shell`
- `shell` is a terminal application used to interface with an operating system through written commands.
- `Bash` is a popular default shell on Linux and macOS.

## Algorithm

_Note: The types of algorithms mentioned in the lesson are supplementary to know._

## The common Big O Notations

Factory Pattern
Singleton Pattern
Day 4
_NOTE: You will not be assessed over the algorithm implementation details. Understand them at a high level._
Bubble Sort
Merge Sort
Binary Search
Linear Search
