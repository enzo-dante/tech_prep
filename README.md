# Big O Notation

TIME COMPLEXITY:

independent of hardware, the worst-case number of steps required for an algorithm (a consistently repeatable sequence of steps) to perform successfully.

SPACE COMPLEXITY:

the total memory space required for an algorithm to successfully complete comprised of the input size and the temporary extra memory space (AUXILLARY SPACE).

### 5 Big O Types (best-to-worst)

O(1) CONSTANT time complexity

- pronounced: O of 1

O(logn) LOGARITHMIC time complexity

- pronounced: O of log n to the base 2

O(n) LINEAR time complexity 

- pronounced: O of n

O(nlogn) loglinear time complexity

- pronounced: O of n log n

O(n^2) QUADRATIC time complexity

- pronounced: O of n-squared

# Serialization

SERIALIZATION: the conversion of a Java object into a static stream (sequence) of bytes, which we can then be saved to a database or transfer over a network.

TRANSIENT: use transient keyword to ignore class fields during serialization that do not represent the state of the object or for any non-serializable references
```
public class Book implements Serializable {

    private static final long serialVersionUID = -2936687026040726549L;
    private String bookName;

    private transient String description;
    private transient int copies;
    
    // getters and setters
}
```

SERIALIZE & DESERIALIZE

The serialization process is instance-independent; classes that are eligible for serialization need to implement Serializable interface.

```
    /**
     * Call the ObjectOutputStream() which takes a serializable object and converts it into a sequence (stream) of bytes. 
     */
    public static void serialize(Book book) throws Exception {

        FileOutputStream file = new FileOutputStream(fileName);
        ObjectOutputStream out = new ObjectOutputStream(file);

        out.writeObject(book);

        out.close();
        file.close();
    }

    /**
     * Call the ObjectInputStream() reads a stream of bytes and converts it back into a Java object.
     * It can then be cast back to the original object.
     */
    public static Book deserialize() throws Exception {

        FileInputStream file = new FileInputStream(fileName);
        ObjectInputStream in = new ObjectInputStream(file);

        Book book = (Book) in.readObject();

        in.close();
        file.close();

        return book;
    }
```

```
    @Test
    void bookSerialization() {

        Book book = new Book();

        book.setBookName("Java Reference");
        book.setDescription("will not be saved");
        book.setCopies(25);

        // the bookName has been properly persisted.
        assertEquals("Java Reference", book.getBookName());

        // the copies field has value 0 and the description is null instead of the original values.
        assertEquals(0, book.getCopies());
        assertNull(book.getDescription());
    }
```

# Recursion

RECURSIVE FUNCTIONS: a continuously self-calling algorithm & each call on the call-stack waits for the algorithm to reach a base case/breaking condition for a return value.

```
recursive factorial method

    !3 = 1*2*3 = 6

        recursiveFactorial(3)
                returns recursiveFactorial(2) * 3

        recursiveFactorial(2)
                returns recursiveFactorial(1) * 2

        recursiveFactorial(1)
                returns recursiveFactorial(0) * 1

        recursiveFactorial(0)
                returns 1
```

RECURSIVE BASE CASE: the breaking condition that initiates an upward propagation of return of values for the waiting calls that results in a call-stack resolution or overflow

```
private static int recursiveFactorial(int number) {

    boolean isBaseCase = (number == 0);

    if(isBaseCase) return 1;

    int decrementedNumber = number - 1;

    return recursiveFactorial(decrementedNumber) * number;
}
```

# INTERFACES

an abstract collection of publicly-shared method signatures that MUST be uniquely implemented/@Override for designated classes for standardization via OOP POLYMORPHISM

```
interface ITelephone {

    // define the public 'signature' (only method names & parameters) of the shared behavior used by the set of class
    void powerOn();
    boolean dial(int phoneNumber);

    final String NO_POWER = "No power button";
}

class DeskPhone implements ITelephone {

    // CONSTANTS/static class variables assigned FINAL value before compilation/instantiation
    private static final String RINGING = "Ring ring ring";

    // OOP ENCAPSULATION private class fields
    private int myNumber;
    private boolean isRinging;

    // OOP CONSTRUCTOR that initializes the class fields on class/object instantiation
    public DeskPhone(int myNumber) {
        this.myNumber = myNumber;
        this.isRinging = false;
    }

    // OOP POLYMORPHISM: unique implementation of method for this object despite same signature shared by multiple objects via @Override
    @Override
    public void powerOn() {
        System.out.println(NO_POWER);
    }

    @Override
    public boolean dial(int phoneNumber) {
        System.out.println(RINGING);
        this.isRinging = true;
    }
}
```

# ABSTRACT CLASSES

ABSTRACTION:

defining the inherited signature, WITHOUT implementation

ABSTRACT CLASS

force child subclass OOP INHERITANCE of method, signatures, & parent super-class fields for a set of classes

- This is achieved by mandating OOP POLYMORPHISM method signatures to be defined in order to execute respectively-unique implementation

  - CANNOT instantiate an ABSTRACT CLASS, must use a normal class that inherits from ABSTRACT CLASS for instantiation

OOP INHERITANCE:

child subclass inherits public class fields + methods from extending parent super class

```
// abstract keyword = no logic, only define the class or method signature shared across adhering classes
abstract class AbstractAnimal {
    
    private String name;

    public AbstractAnimal(String name) {
        this.name = name;
    }

    public abstract void eat();

    public String getName() {
        return this.name;
    }
}

// OOP INHERITANCE: child-class constructor needs to extend parent super-class Animal in addition to abstract class method implementation
class Dog extends AbstractAnimal {

    private String color;

    public Dog(String color, String name) {
        super(name);
        this.color = color;
    }

    @Override
    public void eat() {
        System.out.println(super.getName() + " is eating");
    }

    public String getColor() {
        return this.color;
    }
}
```

# INTERFACES VS ABSTRACT CLASSES

- ABSTRACT CLASSES can have class fields/object instance members AND define abstract publicly-shared signatures

  - CANNOT instantiate an ABSTRACT CLASS, must use a normal class that inherits from ABSTRACT CLASS for instantiation

- INTERFACES can ONLY define publicly-shared signatures

# Concurrency

software that can execute processes simultaneously (one task doesn't have to complete before another one can start)

CONCURRENCY BENEFITS:

- free up the main thread so that it can continue working and executing, you can report progress or accept user input and perform those other tasks on the screen or in other parts of the program, while another long-running task that we kicked off in another thread continues to execute in the background.

- might want to use threads is because an API requires us to provide one.

PROCESS:

an instance of a computer program with its own memory space that's sequentially executed by a computer system that has the ability to run several computer programs concurrently.

```
java virtual machine instance ->
        the JVM runs as a process ->
            running a java console application ->
                we're initiating said PROCESS
```

THREAD:

a unit of execution within a process, each process can have multiple threads, a method for a program to "split" itself into two or more simultaneously or pseudo-simultaneously running tasks.

- every process has a heap and every thread has a thread stack.

```
// THREADS .start(): only JVM executes .run() for a given single Thread (always a new Thread instance), including priority-assigned threads, and CANNOT assume Thread instance execution order
new Thread() {
    @Override
    public void run() {
        System.out.println("Hello from anonymous class Thread")
    }
}.start();
```

MULTITHREADING:

the JVM is multi-processed and multithreaded and has background processes running while a single-thread (main) process/application is executing.

THREAD JOIN:

when we join a thread to a second thread, the first thread will wait for the second thread to terminate or reach timeout value and then it will wake to continue to execute.

```
public static void main(String[] args) {

    // THREADS + GENERIC CLASSES/LAMBDAS: Thread.instance w/ parameter class instance that implements Runnable INTERFACE & immediately .start() no-name instance on it's own thread in the HEAP
    Thread anotherThread = new Thread(new MyRunnableThread());
    anotherThread.start();

    Thread anonymousThread = new Thread(new MyRunnableThread() {
        @Override
        public void run() {

            try {

                // anotherThread.interrupt();


                // THREAD JOIN: And when we join a thread to a second thread, the first thread will wait for the second thread to terminate or reach timeout value and then it will wake to continue to execute.
                int timeout = 2000;
                anotherThread.join(timeout)

                System.out.println("anotherThread terminated or timed out, so I'm running again");

            } catch(InterruptedException e) {
                System.out.println("this.thread counldn't wait...it was interrupted");
            }
        }
    });
    anonymousRunnableThread.start();
    System.out.println("Again, hello from the main Thread");
}

class MyRunnableThread implements Runnable {
    @Override
    public void run() {
        System.out.println("Hello from MyRunnableThread interface implementation of .run()");
    }
}
```

# SYNCHRONIZATION

the process of controlling when threads execute code and therefore when they can access the heap is called synchronization.

- when working with threads, we have to synchronize all areas where we think or where interference can happen.

THREAD SYNCHRONIZATION code blocks:

use synchronization keyword so that all other threads that want to call any synchronized sections in that class will suspend until the single thread running the synchronized code block exits it & passes the object's INTRINSIC LOCK.

```
public synchronized void doCountdown() {
    String color = ThreadColor.ANSI_CYAN;
    String threadName = Thread.currentThread().getName();

    switch(threadName) {
        case THREAD_ONE:
            color = ThreadColor.ANSI_CYAN;
            break;
        case THREAD_TWO:
            color = ThreadColor.ANSI_PURPLE;
            break;
        default: 
            color = ThreadColor.ANSI_GREEN;
            break;
    }
    synchronizedLoop(color, threadName);
}

private void synchronizedLoop(String color, String threadName) {

    synchronized(this) {
        for(int i = 10; i > 0; i--) {
            System.out.println(color + threadName + ": i = " + i);
        }
    }
}
```

DEAD LOCKS:

application freezes during execution due to unreleased INTRINSIC LOCKS - the synchronized shared-resource code executes one at a time and the single running thread is holding the objects INTRINSIC LOCK blocking other threads that WAIT for the lock release via NOTIFY

THREAD SYNCHRONIZATION + DEADLOCKS:

key to avoiding deadlocks when two or more threads will be competing for two or more locks. You want to make sure that all threads or all the threads will try to obtain the locks in the same order.

```
public static Object lock1 = new Object();

private static class Thread1 extends Thread {

    public void run() {

        synchronized(lock1) {

            // THREAD SYNCHRONIZATION + EXCEPTION HANDLING + INTRINSIC REENTRANT LOCK: in TRY-FINALLY code block, use ReentrantLock.lock() to acquire the object's intrinsic lock & execute code one at a time -- other calling threads will suspend until the single running thread calls Reentrant.unlock() to pass the class/object's INTRINSIC LOCK.
            try {
                Thread.sleep(1000);
            } catch(InterruptedException e) {
                System.out.println(e.getMessage());
            }
        }
    }
}
```

ARRAY BLOCKING QUEUE:

a queue is a (FIFO) first-in, first-out abstract class implemented by a LINKED LIST that uses enqueue(), dequeue(), peek()

```
// ArrayBlockingQueue: we have to pass in the number of elements the array should be able to hold
int numElements = 6;

// THREAD SYNCHRONIZATION + EXCEPTION HANDLING + INTRINSIC REENTRANT LOCK: in TRY-FINALLY code block, use ReentrantLock.lock() to acquire the object's intrinsic lock & execute code one at a time -- other calling threads will suspend until the single running thread calls Reentrant.unlock() to pass the class/object's INTRINSIC LOCK.
ArrayBlockingQueue<String> arrayBlockingQueue = new ArrayBlockingQueue<>(numElements);

QueueProducer producer = new QueueProducer(arrayBlockingQueue, ThreadColor.ANSI_YELLOW);
QueueConsumer consumer1 = new QueueConsumer(arrayBlockingQueue, ThreadColor.ANSI_PURPLE);
QueueConsumer consumer2 = new QueueConsumer(arrayBlockingQueue, ThreadColor.ANSI_CYAN);
```

EXECUTOR SERVICE:

optimize a managed set of threads, thus reducing the overhead of thread creation

```
int numThreads = 3;
ExecutorService executorService = Executors.newFixedThreadPool(numThreads);

executorService.execute(producer);
executorService.execute(consumer1);
executorService.execute(consumer2);
```

THREAD POOLS + Future: a return value from an executed thread in a thread pool

THREADS + ANONYMOUS CLASSES/LAMBDA: when using anonymous classes, immediately executing no-name Thread class w/ Thread.subclass parameter that implements Runnable interface to .start() on its own thread in the HEAP

```
Future<String> future = executorService.submit(new Callable<String>() {
    @Override
    public String call() throws Exception {
        return "executorService.submit() was called; this is the result";
    }
});
```

ATOMIC ACTIONS:

once a thread starts these actions, they cannot be suspended during execution, and must complete

- reading and writing reference variables

- reading and writing primitive variables, exception long & double

- reading and writing volatile variables

```
int atomicAction1 = 1;
int atomicAction2 = atomicAction1;
```

VOLATILE VARIABLES:

the JVM writes the value back to main memory immediately after a thread updates the value in its CPU cache, and it also guarantees that every time a variable reads from a volatile variable, it will get the latest value.

```
public volatile int volatileVariable;
```

THREAD STARVATION:

threads aren't given the opportunity to progress due to threat priority - assigning a high priority to a thread means the OS should try and run the thread before other waiting threads.


# Data Structures 

### arrays

O(1) CONSTANT time complexity when getting an element in an array with an index because it always take 3 steps

- step 1: multiply size of the element by its index
- step 2: get the start address of the array
- step 3: add the start address to the result of the multiplication

```
int result = intArray[index];
```

O(n) LINEAR time complexity when getting an element in an array WITHOUT an index

```
for(int index = 0; index < intArray.length; index++) {

    int randomValue = 10;

    if(intArray[index] == randomValue) return intArray[index];
}
```

# sets

sets are a computationally fast unordered collection WITHOUT DUPLICATES implemented via a HASHSET class

```
Set<Integer> numbers = new HashSet<>();
numbers.add(1);
```

SET UNION:

a set (WITHOUT DUPLICATES) that contains ALL elements of 2 or more hashsets via hashSet.addAll()

```
Set<Integer> set1 = new HashSet<>();
Set<Integer> set2 = new HashSet<>();

set1.addAll(set2);
```

.EQUALS & .HASHCODE @Override both methods if using own object as map key or set element

- HASHSET element/ HASHMAP key custom CLASSES: @Override .equals() & .hashcode() methods - if 2 objects compare equal, then they must have same collection bucket hashcode

VENN DIAGRAM ASYMMETRIC DIFF:

remove all shared elements of 1 set found in another set via bulk operation hashSet.removeAll()

```
Set<Integer> set1 = new HashSet<>();
Set<Integer> set2 = new HashSet<>();

set1.addAll(set2);

Set<Integer> asymmetric = new HashSet<>(set1);
asymmetric.removeAll(set2);
```

VENN DIAGRAM SYMMETRIC DIFF:

remove all shared elements found in both sets & return all non-shared elements of both sets (hashSetUnion - hashSetIntersection)

### Singly LinkedLists

Singly LinkedLists w/ an array backing

```
public class EmployeeNode {

    private Employee employee;
    private Employee next;

    public EmployeeNode(Employee employee) {
        this.employee = employee;
    }

    @Override
    public String toString(){
        return this.employee.toString();
    }

    public Employee getEmployee() {
        return this.employee;
    }

    public Employee getNext() {
        return this.next;
    }

    public void setEmployee(Employee employee) {
        this.employee = employee;
    }

    public void setNext(Employee employee) {
        this.next = employee;
    }
}
```

HEAD --> { currentNodeValue, nextNodePointer } --> { currentNodeValue, nextNodePointer } --> null

```
public class EmployeeLinkedList {

    private Employee head;
    private int size;

    public EmployeeLinkedList() {
        this.head = null;
        this.size = 0;
    }

    public boolean isEmpty() {
        return this.head == null;
    }

    public void printList() {

        EmployeeNode currentNode = this.head;


        System.out.print("HEAD <--> ");

        while(currentNode != null) {
            System.out.print(currentNode);
            System.out.print("<-->");

            currentNode = currentNode.getNext();
        }
        System.out.print("<--> null");
        System.out.println("size: " + this.size);
    }

    /**
     * O(1) CONSTANT time complexity when adding node to the front of a list since index will always be 0
     * O(n) LINEAR space complexity when adding node to a list to account for new field in memory 
     */
    public void addToFront(Employee employee) {

        if(employee == null) return;

        // instantiate a new node that will serve as the new head of the linkedList
        EmployeeNode node = new EmployeeNode(employee);

        // set the current head as the new node's next value (shift current head down 1 node)
        node.setNext(this.head);

        // set new node as new head
        this.head = node;

        // increment length of linkedList
        this.size++;
    }

    /**
     * O(1) CONSTANT time complexity when removing node to the front of a list since index will always be 0
     * O(1) CONSTANT space complexity when removing node from a list 
     */
    public EmployeeNode pop() {

        if(this.isEmpty()) return null;

        // save removed node 
        EmployeeNode removedNode = this.head;

        // set head as next node of current head that is going to be removed
        this.head = removedNode.getNext();

        this.size--;

        removedNode.setNext(null);
        return removedNode;
    }

    public int getSize() {
        return this.size;
    }

    public EmployeeNode getHead() {
        return this.head;
    }
}
```

### Doubly LinkedLists

Doubly LinkedLists w/ an array backing

```
public class EmployeeNode {

    private Employee employee;
    private Employee next;
    private Employee previous;

    public EmployeeNode() {
        this.head = null;
        this.next = null;
        this.tail = null;
    }

    @Override
    public String toString() {
        return this.employee.toString();
    }

    public Employee getEmployee() {
        return this.employee;
    }

    public Employee getNext() {
        return this.next;
    }

    public Employee getPrevious() {
        return this.previous;
    }

    public void setEmployee(Employee employee) {
        this.employee = employee;
    }

    public void setNext(Employee employee) {
        this.next = employee;
    }

    public void setPrevious(Employee employee) {
        this.previous = employee;
    }
}
```

null --> HEAD <--> {previousPointer, currentNodeValue, nextNodePointer } <--> {previousPointer, currentNodeValue, nextNodePointer } <--> TAIL --> null

```
public class DoublyLinkedList {

    private Employee head;
    private Employee tail;
    private int size;

    public DoublyLinkedList() {
        this.head = null;
        this.tail = null;
        this.size = 0;
    }

    public boolean isEmpty() {
        return this.head == null;
    }

    public void printList() {

        EmployeeNode currentNode = this.head;
        System.out.print("HEAD <--> ");

        while(currentNode != null) {
            System.out.print(currentNode);
            System.out.print("<-->");

            currentNode = currentNode.getNext();
        }

        System.out.print("<--> null");
        System.out.println("size: " + this.size);
    }

    /**
     * O(1) CONSTANT time complexity when adding node to the front of a list since index will always be 0
     * O(n) LINEAR space complexity when adding node to a list to account for new field in memory 
     */
    public void addToFront(Employee employee) {

        // instantiate a new node that will serve as the new head of the linkedList
        EmployeeNode newNode = new EmployeeNode(employee);

        if(isEmpty()) {

            // if the linkedList is empty, then new node will serve as head and tail
            this.tail = newNode;

        } else {

            // If list is NOT empty, set the current head node's previous pointer to the new node. 
            this.head.setPrevious(newNode);

            // set the current head as the new node's next value (shift current head down 1 node)
            newNode.setNext(this.head);
        }

        // establish new doubly-linked node as new head
        this.head = newNode;

        // increment size of doubly linkedList
        this.size++;
    }

    /**
     * O(1) CONSTANT time complexity when adding node to the front of a list since index will always be last
     * O(n) LINEAR space complexity when adding node to a list to account for new field in memory 
     */
    public void addToEnd(Employee employee) {

        // instantiate a new node that will serve as the new head of the linkedList
        EmployeeNode newNode = new EmployeeNode(employee);

        if(isEmpty()) {

            // if the linkedList is empty, than added node will serve as head and tail
            this.head = newNode;

        } else {

            // If list is NOT empty, set the current tail node's doubly next pointer to the new node. 
            this.tail.setNext(newNode);

            // set the current tail as the new node's previous value (shift current tail up 1 node)
            newNode.setPrevious(this.tail);
        }

        // establish new doubly-linked node as new tail
        this.tail = newNode;

        // increment size of doubly linkedList
        this.size++;
    }

    /**
     * O(1) CONSTANT time complexity when removing node from the front of a list since index will always be 0
     * O(1) CONSTANT space complexity when removing node from a list 
     */
    public EmployeeNode removeFromFront() {

        if(isEmpty()) return null;

        EmployeeNode removedNode = this.head;

        boolean hasOnlyOneNode = this.head.getNext() == null;

        if(hasOnlyOneNode) {

            // set tail to null to facilitate linkedList emptiness 
            this.tail = null;

        } else {

            // if linkedList has more than 1 node, set current head's nextNode previous pointer to null
            this.head.getNext().setPrevious(null);
        }

        // establish new head
        this.head = this.head.getNext();

        // decrement size of linkedList
        this.size--;

        removedNode.setNext(null);
        return removedNode;
    }

    /**
     * O(1) CONSTANT time complexity when removing node from the front of a list since index will always be 0
     * O(1) CONSTANT space complexity when removing node from a list 
     */
    public EmployeeNode removeFromEnd() {

        if(isEmpty()) return null;

        EmployeeNode removedNode = this.tail;
        boolean hasOnlyOneNode = (this.tail.getPrevious() == null);

        if(hasOnlyOneNode) {

            // set head to null to facilitate linkedList emptiness 
            this.head = null;

        } else {

            // if linkedList has more than 1 node, set current tail's previousNode next pointer to null
            this.tail.getPrevious().setNext(null);
        }

        // establish new tail
        this.tail = tail.getPrevious();
        this.size--;

        removedNode.setPrevious(null);
        return removedNode;
    }

    public int getSize() {
        return this.size;
    }

    public EmployeeNode getHead() {
        return this.head;
    }

    public EmployeeNode getTail() {
        return this.tail;
    }
}
```

# Stacks

STACKS: an abstract class that only accesses variables from the top/front on a stack because it's a last-in, first-out (LIFO) data structure implemented by a LINKED_LIST or ARRAY

- O(n) linear TIME COMPLEXITY: due to LIFO (only accessed from the top/front), array STACK for push(), pop(), peek()

- O(1) constant TIME COMPLEXITY: due to LIFO (only accessed from the top/front), linkedList STACK for push(), pop(), peek()

```
class ArrayStack {

    // private class fields
    private Employee[] stack;

    // STACK top: always null because it's a placeholder for next potential item; actual top of stack is the last index of the array
    private int top;

    // OOP CONSTRUCTOR that initializes the class fields & INTRINSIC LOCK on class/object instantiation
    public ArrayStack(int capacity) {

        this.stack = new Array[capacity]
        this.top = 0;
    }

    // OOP CLASS METHODS: unique object behavior
    public int isEmpty() {
        return this.top == 0;
    } 

    /**
     * get object at top/front of stack but do not remove
     */
    public Employee peak() {

        // EXCEPTION HANDLING look before you leap: use if-else statement to handle errors
        if(this.isEmpty()) throw new EmptyStackException();

        int firstIndex = this.top - 1;
        return this.stack[firstIndex];
    }

    public void push() {

        boolean isFullForResize = this.top == this.stack.length;

        if(isFullForResize) {

            // double array size
            int doubleArraySize = this.stack.length * 2;
            Employee[] resizedArray = new Array[doubleArraySize];

            // copy elements of stack's old array into new resized array
            int startIndex = 0;
            System.arraycopy(this.stack, startIndex, resizedArray, startIndex, doubleArraySize);

            // set stack's backing array to resized array
            this.stack = resizedArray;
        }

        // add new object to top of stack
        this.stack[this.top++] = employee;
    }

    public Employee pop() {

        // THROW EXCEPTION: initiate specific exception with provided error msg
        if(this.isEmpty()) throw new EmptyStackException();


        // STACK top: the actual top of stack is the last index of the array
        int indexLIFO = --this.top;
        Employee poppedEmployee = this.stack[indexLIFO];

        // STACK top is always null because it's a placeholder for next potential item
        this.stack[this.top] = null;

        return poppedEmployee;
    }

    // GETTERS & SETTERS
    public Employee[] getStack() {

        for(int i = 0; i < this.stack.length; i++) {
            System.out.println(this.stack[i]);
        }

        return this.stack;
    }
}
```

# Maps

MAPS: an INTERFACE of unique_key-value pairs implemented by the HASHMAP or LINKED HASHMAP classes with 2 GENERIC parameters

- O(1) CONSTANT time complexity: getting a map value with a key will always take the same number of steps (3)

```
// GENERICS: improve OOP ENCAPSULATION by creating classes, interfaces, & methods that only take a specific dataType parameter;
Map<String, String> languages = new HashMap<>();

String key = "English";
String value = "Primary language in the United States";

```

add unique_key-value generics class pair into map collection

```
// re-adding the map key will override the old value 
languages.put(key, value) 
```

retrieve record via key in map collection

```
languages.get(key)
```

get the value mapped with specified key. If no value is mapped with the provided key then the default value is returned

```
languages.getOrDefault(key, defaultValue)
```

validate key existence in map before adding/update key in map

```
languages.containsKey(key)
```

# Queues 

QUEUES: an abstract class that only accesses variables from the top/front on the queue because it's a first-in, first-out (FIFO) data structure implemented by a LINKED_LIST or ARRAY

- O(n) linear TIME COMPLEXITY: due to FIFO (only accessed from the top/front), array QUEUES for add(), pop(), peek()

- O(1) constant TIME COMPLEXITY: due to FIFO (only accessed from the top/front), linkedList QUEUES for add(), pop(), peek()

CIRCULAR QUEUE: wrap queue back-to-front, where back field is always pointing to next available queue position

```
class CircularQueue {

    private Employee[] queue;
    private int front;
    private int back;

    public CircularQueue(int capacity) {

        this.queue = new Employee[capacity]
        this.front = 0;
        this.back = 0;
    }

    public int getSize() {

        boolean isWrapped = this.front <= this.back;
        int wrappedSize = this.back - this.front;

        if(isWrappedQueue) return wrappedSize; 

        // to handle negative number when wrapped circular queue size, wrapped queue numElements is add queueLength to wrappedSize 
        return (wrappedSize + this.queue.length);
    }


    /**
     * O(1) constant time complexity: preview only first item at the front of the queue
     */ 
    public Employee peek() {

        // THROW EXCEPTION: initiate specific exception with provided error msg
        if(this.getSize() == 0) return throw new NoSuchElementException();

        return this.queue[this.front];
    }

    /**
     * O(1) constant time complexity: adding to a full circular queue needs to be resized/doubled
     */ 
    public void add(Employee employee) {

        if(employee == null) return;

        int lastIndex = this.queue.length - 1;
        boolean isFullAndResize = this.getSize() == lastIndex; 

        if(isFullAndResize) {

            int doubleCapacity = 2 * this.queue.length;
            Employee[] resizedArray = new Employee[doubleCapacity]

            // when necessary to resize array, unwrap wrapped circular queue by copy elements at the front the end of the array
            int copyStart = 0;
            int copyEnd = this.queue.length - this.front;

            System.arraycopy(this.queue, this.front, resizedArray, copyStart, copyEnd);
            /*
                0 - jane            ->      0 - mike
                1 - john            ->      1 - bill
                2        - back     ->      2        - back
                3 - mike - front    ->      3 - mike - front
                4 - bill            ->      4 - bill
             */

             System.arraycopy(this.queue, copyStart, resizedArray, copyEnd, this.back)
             /*
                0 - mike            ->      0 - mike - front
                1 - bill            ->      1 - bill
                2        - back     ->      2 - jane
                3 - mike - front    ->      3 - john
                4 - bill            ->      4 - addItem
                                            5        - back
                                            6
                                            7
             */

            this.queue = resizedArray;
        }

        // add object to the back of the queue
        this.queue[this.back] = employee;

        int lastQueueIndex = this.queue.length - 1; 
        boolean isWrapped = this.back <= lastQueueIndex;

        this.back = isWrapped ? this.back + 1 : 0; 
    }

    /**
     * O(1) constant time complexity: remove first item that is at the front of the queue
     */ 
    public Employee pop() {

        // ! THROW EXCEPTION: initiate specific exception with provided error msg
        if(this.getSize() == 0) throw new NoSuchElementException();

        // FIFO: get employee at the front of the queue
        Employee employee = this.queue

        // null-out first index and move queue front index up by 1
        this.queue[this.front] = null;
        this.front++;

        boolean isEmptyQueue = this.getSize() == 0;
        boolean isFullyWrapped = this.front == this.queue.length;

        // if queue is empty after removal of front: reset queue
        if(isEmptyQueue) {

            this.back = 0;
            this.front = 0;

        } else if(isFullyWrapped) {

            // if queue fully wrapped, set front back to index 0 because no more unused space in queue
            this.front = 0;
        }

        return employee;
    }
}
```

# Binary Trees

BINARY TREE:

a collection of 1 parent node to respective 2 children nodes with parent child connection edges and left-to-right node movement depends on child value comparisons

```
public static BinaryTree buildTree() {

    BinaryTree binaryTree = new BinaryTree();
    
    binaryTree.insertNode(25);
    binaryTree.insertNode(20);
    binaryTree.insertNode(15);
    binaryTree.insertNode(27);
    binaryTree.insertNode(30);
    binaryTree.insertNode(29);
    binaryTree.insertNode(26);
    binaryTree.insertNode(22);
    binaryTree.insertNode(32);

    return binaryTree;
}
```

LEVEL-ORDER TRAVERSAL

left-to-right recursively traverse down binary tree for node value by comparing the current node's 2 child values

    level order: [25, 20, 27, 15, 22, 26, 30, 29, 32]

                        25

                   20       27

              15    22        26  30

                                    29 32

PRE-ORDER TRAVERSAL:

visit the main root first, next the root of the subtree, children left-to-right, and repeat

    pre-order: [25, 20, 15, 22, 27, 26, 30, 29, 32]

                        25

                   20       27

              15    22        26  30

                                    29 32

POST-ORDER TRAVERSAL:

visit the root of every subtree last left-to-right, and repeat

    post-order: [15, 22, 20, 26, 29, 32, 30, 27, 25]

                        25

                   20       27

              15    22        26  30

                                    29 32

IN-ORDER TRAVERSAL:

visit the left-child, then root, then right-child, and repeat 

    in-order: 15, 20, 22, 25, 26, 27, 29, 30, 32

                       25

                  20       27

             15    22        26  30

                                   29 32

```
class BinaryTree {

    // CONSTANTS/static class variables assigned FINAL value before compilation/instantiation
    private static final String EMPTY_TREE = "This binary tree is empty";
    private static final String IN_ORDER_TRAVERSAL = "In-order Traversal";

    // OOP ENCAPSULATION private class fields
    private TreeNode root;

    // OOP CONSTRUCTOR that initializes the class fields & INTRINSIC LOCK on class/object instantiation
    public BinaryTree() {
        this.root = null;
    }

    // CLASS METHODS: unique object behavior
    // ACCESS-MODIFIER protected: accessibility the variable or method is limited to the scope of the defining class & it's OOP INHERITANCE subclasses within the package
    public boolean isEmpty() {
        return this.root == null;
    }

    public void traverseInOrder() {

        if(isEmpty()) return;

        System.out.println(IN_ORDER_TRAVERSAL);
        this.root.traverseInOrder();
    }

    public void insertNode(int value) {
        if(isEmpty()) {
            this.root = new TreeNode(value);
        } else {
            this.root.insertNode(value);
        }
    }

    // METHOD OVERLOADING: use same name, but with unique parameters, for related methods to reduce tech debt and optimize readability & scalability
    public void delete(int value) {
        this.root = delete(this.root, value);
    }

    /*
       ! BINARY TREE DELETE TRAVERSAL: recursively traverse binary tree for position of node to delete, delete node, and shift replacement node into position to maintain sorted order & maintain tree integrity

           * original:
                                    25

                              20       27

                         15    22        26  30

                         17                     29 32

           ? delete node is a leaf: null out parent node's left or right child

           * null out 17
                                    25

                              20       27

                         15    22        26  30

                                               29 32

           ? delete node has one child: save leaf value, delete leaf &  replace its value at the respective parent node

           * deleted 17 and replaced parent node value 15 with 17

                                    25

                              20       27

                         17    22        26  30

                                             29 32

           ? delete node has two children: get the largest value in left-subtree or the smallest value in right-subtree

           step 1: look for replacement node for minimal disruption from EITHER (NOT both) left or right subtree

           step 2a: if left subtree selected, take the largest value from the left subtree

                   * deleteTargetNode: 20
                   * subTreeRoot: 15

                   * look for replacementNode starting at the root of the subtree of the deleteTargetNode (the max in leftSubtree)
                   * max: completely traverse left edges of a left subtree until discovering a node without a right child
                   * max: 17
                       if 17 had a left child, 17 replaces 20 & the left child replaces 17 node value

                   * null out node15 child

                                            25

                                      20       27

                                 15    22        26  30

                                 17                     29 32

                   * post-delete
                                            25

                                      17       27

                                 15    22        26  30

                                                        29 32

           step 2b: if right subtree selected, take the largest value from the right subtree

                   * deleteTargetNode: 27
                   * subTreeRoot: 30

                   * look for replacementNode starting at the root of the subtree of the deleteTargetNode (the min in leftSubtree)
                   * min: completely traverse right edges of a right subtree until discovering a node without a left child
                   * min: 29
                       if 29 had a right child, 29 replaces 27 & the right child replaces 29 node value

                   * null out node15 child

                                            25

                                      20       27

                                 15    22        26  30

                                 17                     29 32

                   * post-delete

                                            25

                                      17       29

                                 15    22        26  30

                                                         32
     */
    private TreeNode delete(TreeNode subtreeRoot, int value) {

        // ! RECURSION BASE CASE: the breaking condition that initiates an upward propagation of return values for the waiting calls resulting in call-stack resolution or overflow
        boolean isBaseCase = (subtreeRoot == null);
        if(isBaseCase) return subtreeRoot;

        boolean inLeftChild = (value < subtreeRoot.getData());
        boolean inRightChild = (value > subtreeRoot.getData());

        if(inLeftChild) {

            // ! TREE NODE DELETE: traverse left side + replace subtreeRoot value on delete
            subtreeRoot.setLeftChild(
                    // ! RECURSION: continuously self-calling algorithm & each call waits for a return value until reaching a base case or experiences a stack overflow
                    delete(subtreeRoot.getLeftChild(), value)
            );

        } else if(inRightChild) {

            // ! TREE NODE DELETE: traverse right side + replace subtreeRoot value onDelete
            subtreeRoot.setRightChild(
                    // ! RECURSION: continuously self-calling algorithm & each call waits for a return value until reaching a base case or experiences a stack overflow
                    delete(subtreeRoot.getRightChild(), value)
            );

        } else {

            boolean isEmptyLeftChild = (subtreeRoot.getLeftChild() == null);
            boolean isEmptyRightChild = (subtreeRoot.getRightChild() == null);

            // TREE NODE DELETE: node to delete has 0 or 1 children by always returning replacement node or same node
            if(isEmptyLeftChild) {

                return subtreeRoot.getRightChild();

            } else if(isEmptyRightChild) {

                return subtreeRoot.getLeftChild();
            }

            // ? TREE NODE DELETE case 2: subtreeRoot/deleteTargetNode has 2 children & find min in rightSubtree or max in leftSubtree for replacement & deletion
            int minimumRightLeaf = subtreeRoot.getRightChild().getMin();
            subtreeRoot.setData(minimumRightLeaf);

            // delete the node that has the smallest value from rightSubtree
            int deleteSmallestNode = subtreeRoot.getData();
            subtreeRoot.setRightChild(delete(subtreeRoot.getRightChild(), deleteSmallestNode));
        }
        return subtreeRoot;
    }

    public int getMin() {
        if(isEmpty()) {
            System.out.println(EMPTY_TREE);
            return Integer.MIN_VALUE;
        } else {
            return this.root.getMin();
        }
    }

    public int getMax() {
        if(isEmpty()) {
            System.out.println(EMPTY_TREE);
            return Integer.MIN_VALUE;
        } else {
            return this.root.getMax();
        }
    }

    public TreeNode getNode(int value) {
        // EXCEPTION HANDLING look before you leap: use if-else statement to handle errors
        if(isEmpty()) return null;

        return this.root.getNode(value);
    }

    // OOP GETTERS & SETTERS
    public TreeNode getRoot() {
        return this.root;
    }

    // INNER CLASS: logically grouped components within an extending parent super class
    protected class TreeNode {

        // OOP ENCAPSULATION private class fields
        private int data;
        private TreeNode leftChild;
        private TreeNode rightChild;

        // OOP constructor that initializes the class fields on class/object instantiation
        public TreeNode(int data) {
            this.data = data;
        }

        // OOP CLASS METHODS: unique object behavior
        /**
         * get values lowest-to-highest by traversing the left-child, then root, then right-child, and repeat
         */
        public void traverseInOrder() {

            boolean hasLeftChild = (this.leftChild != null);

            if(hasLeftChild) {
                this.leftChild.traverseInOrder();
            }

            System.out.print(this.data + ", ");

            boolean hasRightChild = (this.rightChild != null);

            if(hasRightChild) {
                this.rightChild.traverseInOrder();
            }
        }

        /**
         * recursively traverse down binary tree left-to-right for insertion node position by comparing the current node's left & right child values
         * @return searched node or null
         */
        public void insertNode(int value) {

            // No duplicate values allowed in implementation
            boolean isDuplicateValue = (value == this.data);

            if(isDuplicateValue) return;

            boolean inLeftChild = (value < this.data);

            if(inLeftChild) {

                boolean foundInsertionLeftNode = (this.leftChild == null);

                if(foundInsertionLeftNode) {

                    this.leftChild = new TreeNode(value);

                } else {

                    // ! RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)
                    this.leftChild.insertNode(value);
                }
            } else {

                boolean foundInsertionRightNode = (this.rightChild == null);

                if(foundInsertionRightNode) {

                    this.rightChild = new TreeNode(value);

                } else {

                    // ! RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)
                    this.rightChild.insertNode(value);
                }
            }
        }

        /**
         * left-to-right recursively traverse down binary tree for node value by comparing the current node's 2 child values
         *
         * @return searched node or null
         */
        public TreeNode getNode(int value) {

            // ! RECURSION BASE CASE: the breaking condition that initiates an upward propagation of return values for the waiting calls resulting in call-stack resolution or overflow
            boolean isBaseCase = (value == this.data);

            if(isBaseCase) return this;

            boolean inLeftChild = (value < this.data);

            if(inLeftChild) {

                boolean hasLeftChild = (this.leftChild != null);

                if(hasLeftChild) {
                    // ! RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)
                    return this.leftChild.getNode(value);
                }

            } else {

                boolean hasRightChild = (this.rightChild != null);

                if(hasRightChild) {
                    // ! RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)
                    return this.rightChild.getNode(value);
                }
            }
            return null;
        }

        /**
         * left-to-right recursively traverse down binary tree for LEFT-MOST node with min value
         * @return min value
         */
        public int getMin() {

            // ! RECURSION BASE CASE: the breaking condition that initiates an upward propagation of return values for the waiting calls resulting in call-stack resolution or overflow
            boolean isBaseCase = (this.leftChild == null);

            if(isBaseCase) {
                return this.data;
            }

            // ! RECURSION: continuously self-calling algorithm & each call waits for a return value until reaching a base case or experiences a stack overflow
            return this.leftChild.getMin();
        }

        /**
         * left-to-right recursively traverse down binary tree for RIGHT-MOST node with max value
         * @return max value
         */
        public int getMax() {

            // ! RECURSION BASE CASE: the breaking condition that initiates an upward propagation of return values for the waiting calls resulting in a call-stack resolution or overflow
            boolean isBaseCase = (this.rightChild == null);

            if(isBaseCase) {
                return this.data;
            }

            // ! RECURSION: continuously self-calling algorithm & each call waits for a return value until reaching a base case or experiences a stack overflow
            return this.rightChild.getMax();
        }

        // OOP GETTERS & SETTERS
        public int getData() {
            return this.data;
        }

        public void setData(int data) {
            this.data = data;
        }

        public TreeNode getLeftChild() {
            return this.leftChild;
        }

        public void setLeftChild(TreeNode leftChild) {
            this.leftChild = leftChild;
        }

        public TreeNode getRightChild() {
            return this.rightChild;
        }

        public void setRightChild(TreeNode rightChild) {
            this.rightChild = rightChild;
        }
    }
}
```

# Graphs

# Linear Search 

traversal beginning to end by incrementing the index by 1 until in the array data structure with O(n) linear time complexity

```
public static int linearSearch(int[] nums, int value) {

    for(int index = 0; index < nums.length; index++) {

        if(nums[index] == value) {
            return index;
        }
    }
    return -1;
}
```

# Binary Search

```
searchValue = 55

    [-22, -15, 1, 7, 20, 35, 55] where midpoint: 7

        [7, 20, 35, 55] where midpoint: 35

            [35, 55] where midpoint == searchValue (55)

                return 55
```

pre-sorted array traversal & recursively divide array into LEFT/RIGHT partitions, until respective middle element equals search value

O(logn) logarithmic TIME COMPLEXITY: keep dividing sorted array in half

```
public static int binarySearch(int[] nums, int value) {

    // STEP 1: initialize pointers at the start and end of an array
    int start = 0;
    int end = nums.length;

    // STEP 2: recursively divide the array down the middle into 2 partitions
    return recursivePartition(nums, start, end, value);
}

private static int recursivePartition(int[] nums, int start, int end, int searchValue) {

    // STEP 4: recursive calls will gradually traverse down to a sorted one-element partition and either return found searchValue or null
    boolean isBaseCase = (start >= end)

    if(isBaseCase) return -1;

    // STEP 3: compare middle element against searchValue
    int midpoint = (start + end) / 2

    boolean foundSearchValue = nums[midpoint] == searchValue;

    /*
        leftP = lesser values respective to parent node midpoint

        rightP = greater values respective to parent node midpoint
    */
    boolean inLeftPartition = nums[midpoint] < searchValue;

    if(foundSearchValue) {

        return midpoint;

    } else if(inLeftPartition) {

        int indexRight = midpoint + 1;
        int start = 0;

        return recursivePartition(nums, indexRight, end, searchValue);

    } else { 
        
        // in rightPartition
        int indexLeft = midpoint - 1;

        return recursivePartition(nums, 0, indexLeft, searchValue);
    }
}
```

# Algorithm Sort

```
public static void swapValues(int[] array, int i, int j) {

    if(i == j) return;

    int tempDisplaced = array[i];

    array[i] = array[j];
    array[j] = tempDisplaced;
}
```

BUBBLE SORT:

```
[[unsortedPartition][]] -> [[unsortedPartition][sortedPartition]]
```

TIME COMPLEXITY O(n-squared) = worst performing nested loops, each loop corresponds to n in Big-O notation, thus O(n^2)

SPACE COMPLEXITY: in-place algorithm that doesn't use extra memory

STABLE ALGORITHM: if there are duplicate elements, the original order of these elements will be preserved

- only swap if index_i > (index_i + 1)

BUBBLE SORT LOGIC:

bubble sort breaks the array into 2 partitions:

- sorted and unsorted

bubble the largest element to the top/unsorted partition that grows with each loop

- right-to-left sorted partition growth

```

public static void bubbleSort(int[] array) {

    // sorted partition
    for(int lastUnsortedIndex = array.length - 1; lastUnsortedIndex > 0; lastUnsortedIndex--) {

        // unsorted partition
        for(int i = 0; i < lastUnsortedIndex; i++) {

            // comparison index
            int j = i + 1;

            // right-to-left sorted partition growth
            if(array[i] > array[j]) {
                swapValues(array, i, j);
            }
        }
    }
    System.out.println(Arrays.toString(array));
}
```

SELECTION SORT

```
[[unsortedPartition][]] -> [[unsortedPartition][sortedPartition]]
```

TIME COMPLEXITY O(n-squared) = worst performing nested loops, each loop corresponds to n in Big-O notation, thus O(n^2)

SPACE COMPLEXITY: in-place algorithm that doesn't use extra memory

STABLE ALGORITHM: if there are duplicate elements, the original order of these elements will be preserved

- only swap if index_i > (index_i + 1)

SELECTION SORT LOGIC:

selection sort breaks the array into 2 partitions:

- sorted and unsorted: the arrays starts unsorted & unsorted partition shrinks from left to right

```
[[unsortedPartition][]] -> [[unsortedPartition][sortedPartition]]
```

selection sort looks for the largest element in the unsorted partition
- swap the largest element found with last element in the unsorted partition via respective index
- then decrement the lastUnsortedIndex var by 1 and repeat the process

```
public static void selectionSort(int[] array) {

    // last index in the given iteration of the unsorted partition (array starts as unsorted)
    int lastUnsortedIndex = array.length - 1;

    // largest value in the given iteration of the unsorted array
    int currentLargestIndex = 0;

    // UNSORTED PARTITION
    for(int index = 0; index <= lastUnsortedIndex; index++) {

        boolean isTraversingUnsortedArray = (index != lastUnsortedIndex);
        if(isTraversingUnsortedArray) {

            // track index with largest element
            if(array[currentLargestIndex] < array[index]) {
                currentLargestIndex = index;
            }
        } else { // reached unsortedPartition end

            boolean foundLargerElement = (array[currentLargestIndex] < array[lastUnsortedIndex]);
            if(foundLargerElement) {

                // if you find a larger value during unsortedPartition traversal, replace currentValue
                currentLargestIndex = lastUnsortedIndex;
            }

            // SORTED PARTITION
            // swap the largest element with element at the end of the unsorted partition
            swapValues(array, currentLargestIndex, lastUnsortedIndex);

            // reset largest element index for next unsortedPartition traversal
            index = 0;
            currentLargestIndex = 0;

            // decrement length of unsorted partition AKA increment length of sorted partition
            lastUnsortedIndex--;
        }
    }
    System.out.println(Arrays.toString(array));
} 
```

# SQL

SQL is a query language, whereas MySQL is a relational database that uses SQL to query a database

<img src="/content/SQLvsNOSQL.png"/>

### RELATIONAL DATABASE:

an interconnected database that holds data tables, a collection of columns (headers) and rows (data)

- you can have multiple tables joined together by a defined relationship

- relationships help force constraints using primary keys and foreign keys

- table constraints: all the data is structured into a uniform manner

- storage is concentrated: 1 node that contains an entire copy of the data, not partitioned by default

- relational db scale can be either:

  - vertical: build a better machine via more memory, faster hard disk, better cpu

  - horizontal: simply add more machines

- relational db access uses raw SQL

### NON-RELATIONAL DATABASES:

collected tables, documents, or graphs hold data together but CANNOT be joined together by a relationship, but organized by key-value stores, that is distributed over multiple servers to be built to scale with high performance & low latency

- best when the data model fits (graphs)

- storage relies on hashing function for the input and the result is used to identify the partition where the data is stored

- nonrelational db scale is easily improved by adding more partitions that function & improved independently

- access: many are no-sql databases that have their own CRUD (create, read, update, delete) functionality that rely on key-value stores

  - REST APIs are used to hit a specific endpoint that comes with certain functionality
