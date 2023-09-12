## Operating System

> What is an operating system?

- main software of a computer it communicates with the hardware and allows other programs to run
- it is comprised of system software, or the fundamental files your computer needs to boot up and function
- they allow you to install and run programs written for the operating system
- the hardware you choose affects the type of operating system it can run:
  - `Windows` on PC hardware
  - `OS X` on Apple's Mac
  - `Linux` on both
- can be interacted with either through `CLI` or `GUI`

### Roles of the Operating System

- `Process Management` (`process` is a program in execution)
- Managing `Threads`
  - a thread is a flow of execution through the process code
  - keeps track of all the instructions that need to be executed next in the program counter
  - contains system registers that hold the current working variables.
  - the thread's stack contains the execution history
- `Scheduling` - in scheduling, the process manager takes the responsibility to remove the running process from the CPU and chooses another process based on a specific strategy.
- `Memory Management` - the functionality of an operating system that handles and manages the primary memory. Processes move back and forth between the main memory and the disk during the execution.

## SOLID Design Principles

> What are the SOLID design principles and why are they important?

- SRP - Single Responsibility Principle
- OCP - Open Closed Principle
- LSP - Liskov Substitution Principle
- ISP - Interface Segregation Principle
- DIP - Dependency Inversion Principle

### `Single Responsibility Principle (SRP)`

- A class should have only one purpose, focusing on a single responsibility or task.
- EXAMPLE: pulling data from a server, manipulating and storing it in a database is not single responsibility

### `Open-Closed Principle (OCP)`:

- Software entities should be open for extension but closed for modification
- you should be able to **add new functionality
  to a system without modifying its existing** code
- we use `abstract classes` and `interfaces` to achieve the `Open Close Principle`
- EXAMPLE: have an abstract area method in a shape class, that can be implemented differentle in triangles and squares, rather than if statements in shape class that have to be modified any time a new shape is introduced

### `Liskov Substitution Principle (LSP)`

- Objects of a superclass should be replaceable with objects of their subclasses
- any instance of a base class should be able to be replaced by an instance of a subclass without affecting the correctness of the program
- This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.
- This is the expected behavior, because when we use inheritance we assume that the child class inherits everything that the superclass has. The child class extends the behavior but never narrows it down.
- EXAMPLE:

### `Interface Segregation Principle (ISP)`

- is about separating interfaces, many client-specific interfaces are better than one general-purpose interface
- Clients should not be forced to depend on interfaces they do not use
- EXAMPLE vehicle interface with opendoors() method and Bike class implementing vehicle interface and mock implement opendoors() method

### `Dependency Inversion Principle (DIP)`

- our classes should depend upon interfaces or abstract classes instead of concrete classes and functions
- if the `OCP (Open Closed Principle)` is the goal of `OO` architecture, `DIP (Dependency Inversion Principle)` is the primary mechanism to achive it

## SDLC

> What is the SDLC? Why is it important?

The `Software Delevopment Life Cycle` (`SDLC`)
is the application of **standard business practices** to building software applications.

- defines workflow for developing software
- reduces costs and mistakes
- has many implementations, like Waterfall and Agile

Benefits:

- reduce cost
- deliver software faster
- meet or exceed customer satisfaction

Stages of SDLC:

- `Planning` - define the scope and purpose of the application.
- `Requirements` - part of planning, includes defining the resources needed to build the project
- `Design` - models the way a software application will work: architecture, user interface, platforms, programming, communications, security, may include `prototyping`
- `Build` - actual writing of the program
- `Document` - may include user guides, troubleshooting guides, and FAQ’s
- `Test`
- `Deploy`
- `Maintain`

### Waterfall

- linear
- one long workflow
- every phase is meticulously detailed and outlined
- not very flexible

#### The advantages of waterfall

- Requires less coordination due to clearly defined phases sequential processes
- A clear project phase helps to clearly define dependencies of work.
  The cost of the project can be estimated after the requirements are defined
- Better focus on documentation of designs and requirements
  The design phase is more methodical and structured before any software is written

#### The disadvantages of waterfall

- Harder to break up and share work because of stricter phase sequences teams are more specialized
- Risk of time waste due to delays and setbacks during phase transitions
  Additional hiring requirements to fulfill specialized phase teams whereas agile encourages more cross-functional team composition.
- Extra communication overhead during handoff between phase transitions
- Product ownership and engagement may not be as strong when compared to agile since the focus is brought to the current phase.

### Agile

- iterative
- short workflows
- flexible

#### The advantages of agile project management

- Faster feedback cycles
  Identifies problems early
- Higher potential for customer satisfaction
- Time to market is dramatically improved
- Better visibility / accountability
- Dedicated teams drive better productivity over time
- Flexible prioritization focused on value delivery

#### The disadvantages of agile

- Critical path and inter-project dependencies may not be clearly defined as in waterfall
- There is an organizational learning curve cost
- True agile execution with a continuous deployment pipeline has many technical dependencies and engineering costs to establish

> When would you use an Agile methodology versus Waterfall?

- when i want to see results faster
- when i want to be flexible

### Agile Core Values

- Individuals and interactions over processes and tools
  - As sophisticated as technology gets, the human element will always serve as an important role in any kind of project management
  - Relying too heavily on processes and tools results in an inability to adapt to changing circumstances.
- Working software over comprehensive documentation
  - As important as documentation is, working software is more. This value is all about giving the developers exactly what they need to get the job done, without overloading them.
- Customer collaboration over contract negotiation
  - Your customers are one of your most powerful assets.
  - Whether internal or external customers, involving them throughout the process can help to ensure that the end product meets their needs more effectively.
- Responding to change over following a plan
  - This value is one of the biggest departures from traditional project management.
  - Historically, change was seen as an expense, and one to be avoided.
  - Agile allows for continuous change throughout the life of any given project. Each sprint provides an opportunity for review and course correction.

#### Key components of Agile project management

- User stories
  - Put simply, a user story is a high-level definition of a work request.
  - It contains just enough information so the team can produce a reasonable estimate of the effort required to accomplish the request.
  - This short, simple description is written from the user’s perspective and focuses on outlining what your client wants (their goals) and why.
  - The user story follows the general format "As a user I want to functionality so that motivation.
    - Example: As a manager, I want to be able to understand my team members' progress, so I can better report our success and failures.
- Sprints
  - Sprints are a short iteration, usually between one to three weeks to complete, where teams work on tasks determined in the sprint planning meeting. As you move forward, the idea is to continuously repeat these sprints until your product is feature ready.
  - Once the sprint is over, you review the product see what is and isn’t working, make adjustments, and begin another sprint to improve the product or service.
  - Sprints are implemented in the Agile framework Scrum but not in some other frameworks like Kanban.
- Stand-up meetings
  - Daily stand-up meetings (under 10 minutes), also known as “daily Scrum meetings,” are a great way to ensure everyone is on track and informed.
  - These daily interactions are known as “stand up” because the participants are required to stay standing, helping to keep the meetings short and to the point.
- Agile board
  - An Agile board helps your team track the progress of your project.
  - This can be a whiteboard with sticky notes, a simple Kanban board, or a function within your project management software.
- Backlog
  - As project requests are added through your intake system, they become outstanding stories in the backlog.
  - During Agile planning sessions, your team will estimate story points to each task.
  - During sprint planning, stories in the backlog are moved into the sprint to be completed during the iteration.
  - Managing your backlog is a vital role for project managers in an Agile environment.

#### Agile Methodology Steps

- Project planning
  - Like with any project, before beginning your team should understand the end goal, the value to the organization or client, and how it will be achieved.
  - You can develop a project scope here, but remember that the purpose of using Agile project management is to be able to address changes and additions to the project easily, so the project scope shouldn’t be seen as unchangeable.
- Product roadmap creation
  - A roadmap is a breakdown of the features that will make up the final product. This is a crucial component of the planning stage of Agile, because your team will build these individual features during each sprint.
  - At this point, you will also develop a product backlog, which is a list of all the features and deliverables that will make up the final product. When you plan sprints later on, your team will pull tasks from this backlog.
- Release planning
  - In traditional waterfall project management, there is one implementation date that comes after an entire project has been developed.
  - When using Agile, however, your project uses shorter development cycles (called sprints) with features released at the end of each cycle.
  - Before kicking off the project, you’ll make a high-level plan for feature releases and at the beginning of each sprint, you’ll revisit and reassess the release plan for that feature.

#### SCRUM

- one implementation of the Agile Metodology
- has actors (product owner, scrum master, etc)
- has ceremonies (events) like:
  - sprint planning
  - daily stand-ups
  - sprint review
- has documents like a burndown chart and backlogs

## HTTP

> What is HTTP? Why is it important to know about?

`HTTP` (`HyperText Transfer Protocol`) is a technique of transmitting data in a particular format, primarily between a server and a

HTTP works by a client making a connection to a `server`, sending a `request`, and receiving a `response`

The data tranmitted can be:

- `hypertext` - A text documents that have the special ability to link to one another.
- `hypermedia` - hypertext documents that have the ability to show multiple kinds of media

A request contains:

- the `method` being used
- the `URL` where the target is
- version of HTTP is being used
- Optional information to help the server with the request (called `headers`)
- For some methods, a `body` which contains some resources (ex.: files to be uploaded)

A response contains:

- version of HTTP is being used
- status code reflecting the outcome of the request
- status message which is shorthand and less descriptive than the status code
- Optional information to detail what happened with the request (called `headers` again)
- For some methods, a body which contains some resource (ex. file to be downloaded)

### HTTP verbs

> What are common HTTP verbs used when a client application is making a request?

- GET
- used to retrieve data from a server at the specified resource
- does not modifying any resources
- safe and `idempotent` method
- POST
- used to send data to the API server to create or update a resource
- the data sent to the server is stored in the request body of the HTTP request
- `non-idempotent`
- PUT
- similar to POST, PUT requests are used to send data to the API to update or create a resource
- `idempotent`, calling the same PUT request multiple times will always produce the same result
- when a PUT request creates a resource the server will respond with a 201 (Created), and if the request modifies existing resource the server will return a 200 (OK) or 204 (No Content)
- HEAD
- DELETE

- deletes the resource at the specified URL

- PATCH
- OPTIONS

### HTTP Status Codes

> What are some common HTTP status codes that can be included in a response?

HTTP Status Codes whether a specific HTTP request has been successfully completed.

Responses are grouped in five classes:

- Informational responses (100–199)
- Successful responses (200–299)
- Redirection messages (300–399)
- Client error responses (400–499)
- Server error responses (500–599)

Common Status Codes:

- 200 - OK, success
- 201 - Created
- 400 - Bad Request, client error
- 404 - Not Found
- 500 - Internal Server Error

## Algorithm

> What is an algorithm?

- step by step instructions for performing a task
- there are many common programming problems, such as:
- finding a value in a group of values
- sorting a group of values

Algorith Types (_SUPPLEMENTARY_):

- recursive
- greedy
- divide and conquer (ex: merge sort)
- backtracking
- branch and bound

### Big 0 Notation

#### Measuring Algorithms

> How would you describe time complexity?

- a reliable way to measure performance of an algorithm is to figure out what its running time tends to be based on when it receives more and more input
- algorithms that slow down if they are given a lot of input don't perform well
- algorithms that still perform fast even if given a lot of input are more ideal
- another thing to consider is that algorithms don't perform exactly the same every time they receive input of the same size
- consider searching 10 values linearly and the correct value is right at the front (best case)
- consider searching 10 values linearly and the correct value is at the back (worst case)
- Big O Notation represents the **worst case** running time of an algorithm as is the most commonly used notation to use to measure

#### Running Time Categories (From Best to Worst)

- `O(1)`: `constant` - runtime is the same regardless of input size.
- `O(log n)`: `logarithmic` - as input increases, runtime doesn't increase too much
- algorithms that are in this category reduce the size of the input it cares about in each step
- `O(n)`: `linear` - as input increases, runtime increases linearly, or at a consistent rate
- algorithms that are in this category perform actions for every value in the input
- example: linear search
- `O(n log n)` : `linearithmic` or quasilinear - as input increases, runtime increases linearly and then some
- algorithms that are in this category could be dividing the input into halves repeatedly, but then performs a linear operation on the results
- example: merge sort
- `O(n^2)`: quadratic. as input increases, runtime increases exponentially
- example: bubble sort

### Search

> What is the difference between linear search and binary search?

#### Linear Search

- `O(n)`
- In a Linear Search, a sequential search is done for all items one by one.
- Every item is checked and if a match is found then that particular item is returned, otherwise the search continues till the end of the data collection.
- Although linear search is generally not the most efficient method of searching an array, it is the best method for searching an unsorted array

#### Binary Search

- for sorted arrays
- If you are searching for an item in a sorted list, then it is possible to eliminate half of the items in the list by inspecting a single item.
- After eliminating half of the initial list, the same process can be repeated to continually cut the list in half until the routine completes by either finding the item, or concluding that the item is not in the list.
- The `time complexity` of the binary search algorithm is `O(log n)`
- The `space complexity` of the binary search algorithm depends on the implementation of the algorithm.
- In the `iterative method`, the space complexity would be `O(1)`.
- The space complexity for the `recursive method` would be O(log n).

### Sort

> What is the difference between Bubble Sort and Merge Sort?

#### Bubble Sort:

- `O(n^2)`
- go through the array to be sorted, compares adjacent elements and swaps them if they are in the wrong order
- by the end of the first round the last element is in the right order
- do it again for n - the last element, now the second to last element is in the right order too

#### Merge Sort:

- `O(nlogn)`
- recursively sorts the array using a `divide-and-conquer` approach.
- the mergeSort function splits the array into two halves, sorts each half recursively using the mergeSort function, and then merges the two sorted halves using the merge function.
- the merge function creates two temporary arrays to hold the left and right sub-arrays, and then merges them back into the original array in sorted order.

## Design Patterns

Design Patterns are tried and true software design for keeping apps maintainable, flexible, and scalable.

### Factory Design Pattern

> What is the Factory design pattern?
> Factory is a design pattern which creates objects in which the precise type may not be known until runtime. There are several reasons to use the factory pattern:

- If you don't know the exact types needed before running the code.
- If you want to hide the creational logic, which prevents end user creating things that they shouldn't.
- If you need an easy way to extend internal components.
- Depending on implementation, the factory pattern can be used to reuse objects, instead of making new ones, which saves space.

Some extra benefits of using the factory pattern:

- Single responsibility is upheld by putting all of the construction code in a single function.
- Open/Closed principle is upheld by allowing new subclasses to easily implement and be added, without negatively affecting any of the already written classes.
- Abstracts the actual creation of the objects away from the user.

#### Real World Application

- Object Creation with Complex Initialization: When an object requires complex initialization or configuration, the Factory Design Pattern can be employed. The factory encapsulates the creation logic and hides the complexity, providing a clean interface for creating objects.

- Dependency Injection: In Dependency Injection frameworks, the Factory Design Pattern is often used to create and manage instances of classes with complex dependencies. The factory can handle the resolution of dependencies and provide the appropriate instances to the requesting components.

- Database Access: In database applications, the Factory Design Pattern can be used to create database connections or data access objects. The factory can handle the creation of the database-specific objects based on the configuration or other criteria.

- Logging: In logging frameworks, the Factory Design Pattern can be used to create logger objects. The factory can determine the appropriate logger implementation based on the specified configuration, such as logging level, destination, or formatting.

- GUI Component Creation: In graphical user interface (GUI) development, the Factory Design Pattern can be employed to create different types of GUI components based on user preferences or application settings. The factory can generate the appropriate components, such as buttons, panels, or dialogs, based on the desired style or behavior.

#### Factory Example

To make a factory:

- Create the abstract data type
- Create several classes that inherit the abstract data type (the objects whose instantiation details may not be known until runtime)
- Set up a static method whose return type is the abstract data type in (1), which will return the concrete instance

```java
// Abstract Data Type
public interface Dessert {}

// Classes that inherit the abstract data type
public class Cake implements Dessert {}

public class Cookie implements Dessert {}

public class IceCream implements Dessert {}

// Good practice to throw an exception if the desired concrete instance is not found
public class DessertNotFoundException extends RuntimeException {}

// Factory class that returns the concrete instance
public class DessertFactory {
    public static Dessert getDessert(String dessertType) {
        switch(dessertType) {
            case "cake":
                return new Cake();
            case "cookie":
                return new Cookie();
            case "ice cream":
                return new IceCream();
            default:
                throw new DessertNotFoundException(dessertType + " not found!");
        }
    }

    public class Demo {
        public static void main(String[] args) {
            Dessert d1 = DessertFactory.getDessert("cake");
            Dessert d2 = DessertFactory.getDessert("cookie");
            Dessert d3 = DessertFactory.getDessert("ice cream");
            Dessert d4 = DessertFactory.getDessert("candy");    // Throws DessertNotFoundException
        }
    }
}
```

#### REV NOTES: About Factory Design Patter:

- creating objects without exposing creation logic to client code
- problem solved by this pattern:
- you have client code keeps track of all available objects it can create
- if you want to create an additional class for client code to use, client code needs to be updated
- solution this pattern provides:
- by removing object creation responsibility from client, client just uses factory to get an object and no longer needs to keep track of concrete classes that it needs to choose from

#### Simple Factory

- not full implementation of the design pattern, but a good first step
- does take responsibility from client
- not flexible
- A class separate from the client class is created to keep track of available options/objects that client code can use
- does not follow Open/Closed Principle since you have to update class if additional option/object added

---

#### Factory Method Pattern (Supplementary)

- does take responsibility from client
- flexible
- Class with client code relies on an abstract factory method. Subclassing superclass allows us to add more options to client code by overriding factory method. Follows Open/Closed Principle.

---

### Singleton Design Pattern

> What is the Singleton design pattern?

- The Singleton design pattern allows for the creation of a single instance of an object in memory that can be shared across multiple classes.
- Benefits of using a Singleton include coordination across the system, clear instance retrieval, control over instantiation, and global access point.
- It can be useful for services in an application, or other resources like a connection or thread pool.
- Situations where Singleton pattern can be useful include logging frameworks, database connections, caching, configuration settings, and thread pool/task manager in concurrent programming.

Singleton Design Patter:

- ensure there can only be one instance of the class and it can be accessed throughout project
- solution this pattern provides:
- for classes where creating more than one object can lead to problems (one logger to ensure your logs are not conflicting/duplicated/out of order)
- when you want the object to exist only when it is needed (for example, you don't want to create a global object from the start of application if it is resource intesive)
- use case we've already seen: connection to a database

#### Benefits to using a Singleton:

- There will only be 1 instance, which allows coordination across a system.
- There is a clear way to fetch the correct instance. getInstance()
- Programmer has complete control over instantiation.
- global access point
- The singleton is not created until it is used, often referred to as lazy instantiation.

#### Drawbacks to using a Singleton:

- Harder to work with in multithreaded environments.
- Different components can be given too much control over other components.

#### Real World Application for Singleton Pattern topic

The primary benefit of a Singleton is the management of data or functionality through a single object in memory. There are many situations in real world applications which may benefit from the implementation of a Singleton, for instance:

- Logging: In logging frameworks, the Singleton Design Pattern can be used to ensure that there is only one instance of the logger throughout the application. This allows different parts of the application to access and use the same logger instance for logging purposes.

- Database Connections: In database applications, the Singleton Design Pattern can be used to manage and share a single database connection instance. This helps in preventing multiple connections to the database, ensuring efficient resource utilization, and providing a centralized access point for database operations.

- Caching: In caching scenarios, the Singleton Design Pattern can be used to maintain a single instance of a cache manager or cache store. This ensures that all parts of the application access the same cache instance and allows for efficient storage and retrieval of frequently accessed data.

- Configuration Settings: In applications that require global access to configuration settings, the Singleton Design Pattern can be used to provide a single instance that holds and manages the configuration data. This allows different parts of the application to access and utilize the configuration settings consistently.

- Thread Pool or Task Manager: In concurrent programming, the Singleton Design Pattern can be used to create a thread pool or task manager with a fixed number of worker threads. This ensures that there is a single instance managing the concurrent tasks or threads, providing control and coordination over the execution.

#### Singleton Example

To make a class into a Singleton in Java use:

- private static variable of the class' type
- private constructor - to prevent arbitrary object creation
- public static getInstance() method, which will either instantiate the object or return the instance in memory

```java
public class Singleton {
    // Private static variable of the class' type
    private static Singleton instance;
    private int number;
    // Private Constructor
    private Singleton() {
        number = 0;
    }

    // Public static getInstance method
    public static Singleton getInstance() {
        if (instance == null)
            instance = new Singleton();
        return instance;
    }
    //this method is called from an instance of the class.
    //However because there is only 1 instance, whenever this is called it will affect all pointers to the instance.
    public void printer(){
        this.number++;
        system.out.println("printer has been called " + this.number + " times.");

    }
}

class Main{
    public static void main(String[] args){
        Singleton mySingle = Singleton.getInstance(); //When this is called the first time the singleton does not exist, so it gets created.
        mySingle.printer(); // output: printer has been called 1 times
        Singleton yourSingle = Singleton.getInstance(); //This time when getInstance is called there already exists an instance, so it just returns the reference to the singleton.
        yourSingle.printer(); // output: printer has been called 2 times
        System.out.println(mySingle == yourSingle); //This will output true, because mySingle points to the same object as yourSingle
    }
}
```
