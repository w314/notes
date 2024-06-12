lifecycle fo object
constructor
body
destructor

lifecycel of application of applet browser programs
init 
service 
destroy

lifecycle of spring bean
init @PostConstruct
service @Bean
destroy @PreDestroy

when would you use multithreading
if several users use your website, each user would be one thread.

In spring boot the tomcat server would handle the multithreading.

gateway? apigee gateway?
how you control how manyusers will enter you server environment? so that it does not crash

you use gateway to control that




if you want to know how many beans are running you would log in @PostConstruct and @PreDestroy

you cannot overwrite static methods




thread

program in execution mode is a process, a task/method in execution mode is a thread

server allocated memory that memory is a thread

thread is a memory management technic
thread is part of process




as task is part of program

without process there is no thread

Threads can be created by overriding the run method of the Runnable Interface.

Runnable is a functional interface with just one abstract method: run.



Is my main method a thread or not?
Yes.

tread priority 1-10 with 5 as default.
Always one thread will start another thread.
What will start the main method's thread?
daemon thread is repsonible to rum main thread.
who will run daemon thread?

WHen you switch on you computer, you are giving electrical pulses that hit your ROM (Read Only Memory) what is in ROM?
Inside ROM we have some assembly style code that start the initial thread of the operating system.

Without ROM your machine won't boot.

As you switch on the computer you see many threads starting, many processes starting. All processes were started by daemong threads.
The daemon threads will start user defined processes.

syncronized?
we use these locks for critical section
intrinsic lock
extrinsic lock

you have critical section only one thread can enter

if you do concurrent programming you have several critical sections

## 
how to decide which thread to exectue critical section?



## Thread LifeCycle
1. New State
```java
Thread t = new Thread();
```
2. Running State (= Critical section ?)
To get my thread into running state.
You request the OS to have your thread to run:
```java
t.start()
```
If you start many thread all the threads get into the `Ready Queeu`



3. Waiting Mode
`wait()`, `sleep()` will make thread to wait
call `notify()` to call thread back to running state

4. Dead Mode
- after thread is done
- value of your thread t will be `null`
- to check if thread is in dead mode use:
```java
// in dead mode value 
t.isAlive()
```



JVM does not have controll over threading.
Operating System will control threads, threads are part of OS.

In what scenario a high priority thread won't execute and a lower priority one does?
If you don't have enough memory to execute a high priority thread, system will swicth to second high priority thread. It that also does not have ....
It will execute the thread it has enough memory for.
If none of them has, it will get to the lowest priority daemon ones.

It will execute the `system.gc()`, it will clean up the garbage using the `.finalize()` method.

Who is responsibel to clean garbages?
Daamon thread

daemon thread is responibel for scheduling


## Multi Threading


Multithreading can be implemented using two main approaches: 
- extending the `Thread Class`
- implementing the `Runnable Interface`

When would you use Thread Class over Runnable Interface?

Servers (TOMCAT, AWS, etc) use `Executor Framework` to handle multithreading. It uses a `Threadpool`

In real life we using the executor framework  to impolement multithreading. Thread class are theory only.

### Extending Thread Class
- limits you inheritance, you cannot extend any other class
- you have to override the `run()` method
- instantiate your class adn start it's `run()` method with calling `start()`
- if my class extends Thread class, any object I create with `new` will be a thread
```java
class MyThread extends Thread {
    public void run() {
        // Code to execute in new thread
    }
}

// Usage
MyThread t = new MyThread();
```
Thread concept
Runnable interface concept


## [Daemon Threads](https://www.geeksforgeeks.org/daemon-thread-java/)
> Low-priority threads that run in the background to perform tasks such as garbage collection or provide services to user threads. 

- serves user thread by performing background tasks
- when all user threads finish execution JVM automatically termintes the daemon thread

Examples
- garbage collection 
- finalizer

Properties
- cannot prevent JVM exit <br>when all user threads finish their execution JVM terminates itself regardless of whether any daemon thread are running
- automatic termination <br>JVM will terminate daemon thread regardless it is still running
- low priority



## Synchronized Keyword

To avoid race condition (in critical section) we have to apply a lock.
Solution:
Add `syncronized` modifier to method signiture. It solves the problem of race condition, locks access to method until the first thread that calls it finishes.

- slows down performance
- threads will not be in sequence (thread started second, can access resource first), but they will have 

- hashtable is thread safe class, it means all its methods are syncronized
- hashmap is not thread safe, it is faster

If a class it thread safe all its methods are synchronized.

circular wait problem also can be solved by locks. (process 1 using deposit and requesting withdrawal, while process 2 uses withdrawal but requesting deposit) You would use the synchronized keyword for both process and withdraw methods.

if we use synchronized on all our methods performance will be slow.

In real life, we do not use the synchronized keyword server will handle multihreading, and we would aks the server if the resource is available

Writing socket programming would teach you how to write multithreading.



_________

why are we calling start() to run run() instead of calling run() directly.

calling run() would execute the thread on the thread we are already on, only start() would start a new thread
calling run() would not be multithreading

start() means you are requesting the OS that you want to call run(), OS will decide when to call run(). Scheduling your thread are the job of the OS.


join concept in thread check it out
if you don't have a join concept

learn executer framework, lock, scheduler



