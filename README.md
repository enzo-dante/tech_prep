# Big O Notation

__TIME COMPLEXITY:__

independent of hardware, the worst-case number of steps required for an algorithm (a consistently repeatable sequence of steps) to perform successfully.

__SPACE COMPLEXITY:__

the total memory space required for an algorithm to successfully complete comprised of the input size and the temporary extra memory space (AUXILLARY SPACE).

### 5 Big O Types (best-to-worst)

O(1) CONSTANT time complexity: worst-case, getting a value with a key will always take the same number of steps (3)

- pronounced: O of 1

O(logn) LOGARITHMIC time complexity: worst-case, using a divide & conquer algorithm to get a value will only slowly increase the number of steps

- pronounced: O of log n to the base 2

O(n) LINEAR time complexity: worst-case, the number of steps is directly proportional to the length of the input size because getting a value WITHOUT a key will require traversing to the end of a collection

- pronounced: O of n

O(nlogn) LOGLINEAR time complexity

- pronounced: O of n log n

O(n-squared) QUADRATIC time complexity: the absolute worst-case, the number of steps exponentially increases due to nested loops.

- pronounced: O of n-squared

# Keywords

__STATIC__

a unique class variable assigned to a single space in memory & referenced across entire application

```
public class Test {

    private static final String NAME = "My name";

    public static void sayMyName() {
        System.out.println(NAME);
    }
}
```

__STATIC INITIALIZATION BLOCKS__

one-time on-initialization execution of 'static {}' and their assigned STATIC FINAL variables

```
private static final String OWNER;
private static final String FIRST_STATIC_MSG;

static {
    OWNER = "Tim";
    FIRST_STATIC_MSG = "STATIC INITIALIZATION BLOCKS: one-time on-initialization execution of 'static {}' and their assigned STATIC FINAL variables";
    System.out.println(FIRST_STATIC_MSG);
}
```

__CONSTANTS__

static class variables assigned FINAL value before compilation/instantiation

```
private static final String POWER_USER = "I am a power user";
```

__METHOD OVERLOADING__

use same name, but with unique parameters, for related methods to reduce tech debt and optimize readability & scalability

```
public int add() {
    return 1 + 1;
}

public int add(int a, int b) {
    return a + b;
}

public int add(int n, String msg) {
    System.out.println(msg);
    return 100 + n;
}
```

__ACCESS-MODIFIERS__

```
public class Person {

    // PRIVATE: access to the variable or method is limited to the scope of the defining class
    private String name;

    // PUBLIC: the variable or method can be accessed from any scope
    public Person(String name) {
        this.name = name;
    }

    // PROTECTED: access to the variable or method is limited to the scope of the defining class & it's OOP INHERITANCE subclasses within the package
    protected String talk() {
        return "This is protected speech";
    }
}

```

__OOP ENCAPSULATION__

use access modifiers to guard the class fields & methods methods from inappropriate external access

```
public class Toy {

    private String name;

    public Toy(String name) {
        this.name = name;
    }

    private int sendError() {
        return -1;
    }

    public String getName() {
        return this.name;
    }
}
```

__OOP INHERITANCE__

child subclass inherits public class fields + methods from extending parent super class

```
public class Animal {

    private String name;

    public Animal(String name) {
        this.name = name;
    }
}

public class Dog extends Animal {

    public Dog(String name) {
        super(name);
    }
}
```

__OOP POLYMORPHISM + INTERFACES__

must implement ALL publicly-shared method signatures via @Override

```
interface ISports {
    void play();
}

public class Player implements ISports {

    private final String name;

    public Player(String name) {
        this.name = name;
    }

    @Override
    public void play() {
        System.out.println("I play sports");
    }
}
```

__OOP COMPOSITION + INNER CLASS__

logically grouped class components within an extending parent super class

```
public class PC {

    private Motherboard motherboard;

    public PC(int ramSlots) {
        this.motherboard = new MotherBoard(ramSlots);
    }

    public Monitor getMonitor() {
        return this.motherboard;
    }

    class Motherboard {

        private int ramSlots;

        public Motherboard(int ramSlots) {
            this.ramSlots = ramSlots;
        }

        public int getRamSlots() {
            return this.ramSlots;
        }
    }
}
```

__EXCEPTION HANDLING__

look before you leap: use if-else statement to handle errors

```
if(n == 0) return false;
```

easier to ask for forgiveness than permission: use try-catch block to handle errors

```
try {
    System.out.println(future.get());
} catch(ExecutionException e) {
    System.out.println(e.getMessage());
} catch(ExecutionException e) {
    System.out.println("Thread running the task was interrupted");
}
```

# Serialization

the conversion of a Java object into a static stream (sequence) of bytes, which we can then be saved to a database or transfer over a network.

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

The serialization process is instance-independent: classes that are eligible for serialization need to implement Serializable interface.

__TRANSIENT__

use transient keyword to ignore class fields during serialization that do not represent the state of the object or for any non-serializable references

```
public class Book implements Serializable {

    private static final long serialVersionUID = -2936687026040726549L;
    private String bookName;

    private transient String description;
    private transient int copies;

    // getters and setters
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

# DIVIDE & CONQUER

recursively divide the original problem into 2 or more sub-problems & repeat until the sub-problems become small enough to solve a base case

- after solving the base case/breaking condition, combine the solutions to construct the overall solution to the original problem

divide & conquer algorithms are great for parallel processing because each sub-problem can be run on a different processor simultaneously (extremely performant on modern systems with large core counts)

```
public class MergeSort {

    private static int[] array = {20, 35, -15, 7, 55, 1, -22};

    public static int[] execute() {
        recursivePartition(array, 0, array.length);
        return array;
    }

    // RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)
    private static void recursivePartition(int[] array, int start, int end) {

        // RECURSIVE BASE CASE: the breaking condition that initiates an upward propagation of return of values for the waiting calls that results in a call-stack resolution or overflow
        int partitionLength = end - start;
        boolean isBaseCase = (partitionLength < 2);

        if(isBaseCase) return;

        // RECURSION + DIVIDE & CONQUER: partition LEFT side FIRST, then RIGHT side with midpoint via start & end indices 
        int midpoint = (start + end) / 2;

        // LEFT partitions
        // [20, 35, -15] ->
        //      [20] [35, -15] ->
        //          [20] [35] [-15]

        recursivePartition(array, start, midpoint);

        // RIGHT partitions 
        // [7, 55, 1, -22] ->
        //      [7, 55] [1,-22] ->
        //          [7] [55] [1] [-22]

        recursivePartition(inputArray, midpoint, end);

        // merging left & right RECURSIVE partitions returns arrays w/ sorted elements
        merge(array, start, midpoint, end);
    }

    private static void merge(int[] array, int start, int midpoint, int end) {

        int leftPartitionEnd = array[midpoint - 1];
        int leftPartitionStart = array[midpoint];

        boolean isAlreadySorted = (leftPartition <= rightPartitionStart);

        if(isAlreadySorted) return;

        int i = start;
        int j = midpoint;
        int tempIndex = 0;

        int tempLength = end - start;
        int tempArray = new int[tempLength];

        // isTraversingLeft = (i < midpoint);
        // isTraversingRight = (j < end);

        while(i < midpoint && j < end) {

            // preserve partition bounds
            int currentLeftElement = array[i];
            int currentRightElement = array[j];

            // MERGE SORT: write smaller of 2 comparison elements to temp array for left-to-right sorted order
            // STABLE ALGORITHM: if equal, write left first to preserve original order

            tempArray[tempIndex++] = (currentLeftElement <= currentRightElement) ? inputArray[i++] : inputArray[j++];
        }

        /*
            MERGE SORT OPTIMIZATION

                LEFT partition remaining elements, must copy to temp array

                RIGHT partition remaining elements, no copying into temp array needed bc already will be in sorted order for input array
         */

        int[] srcArray;
        int destinationIndex = start + tempIndex;
        int remainingElementIndex = i;

        // no action, if no remainder left partition elements, else move to correct index
        int notCopiedCount = midpoint - i;

        // copying sorted tempArray elements back into inputArray
        srcArray = array;
        System.arraycopy(srcArray, remainingElementIndex, array, destinationIndex, notCopiedCount);

        // only copy numElements in tempArray into array
        srcArray = tempArray;
        System.arraycopy(srcArray, 0, array, start, tempIndex);
    }
}
```

__POTENTIAL PROBLEMS__

make sure to avoid redundant recursive calls (solved via MEMOIZATION)

- MEMOIZATION: is a technique that can be used to improve the efficiency of divide & conquer algorithms by storing the solutions to earlier problems & eliminating redundant calls

# Interfaces

an abstract collection of publicly-shared method signatures & public CONSTANTS that MUST ALL be uniquely implemented/@Override for designated classes for standardization via OOP POLYMORPHISM

```
interface ITelephone {

    // define the public 'signature' (only method names & parameters) of the shared behavior & public CONSTANTS used by the set of class
    void powerOn();
    boolean dial(int phoneNumber);

    final String NO_POWER = "No power button";
}

class DeskPhone implements ITelephone {

    private static final String RINGING = "Ring ring ring";

    private int myNumber;
    private boolean isRinging;

    public DeskPhone(int myNumber) {
        this.myNumber = myNumber;
        this.isRinging = false;
    }

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

# Abstract Classes 

__ABSTRACTION__

defining the inherited signature, WITHOUT implementation

__ABSTRACT CLASS__

force child subclass OOP INHERITANCE of method, signatures, & parent super-class fields for a set of classes

- This is achieved by mandating OOP POLYMORPHISM method signatures to be defined in order to execute respectively-unique implementation

  - CANNOT instantiate an ABSTRACT CLASS, must use a normal class that inherits from ABSTRACT CLASS for instantiation

__OOP INHERITANCE__

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

# Interfaces vs Abstract Classes 

- ABSTRACT CLASSES can have class fields/object instance members AND define abstract publicly-shared signatures

  - CANNOT instantiate an ABSTRACT CLASS, must use a normal class that inherits from ABSTRACT CLASS for instantiation

- INTERFACES can ONLY define publicly-shared signatures

# Generics

improve OOP ENCAPSULATION by creating classes, interfaces, & methods that only take a specific dataType parameter

```
ArrayList<Integer> onlyIntegers = new ArrayList<>();
onlyIntegers.add(1);

// not using generics
ArrayList elements = new ArrayList<>();
elements.add(1);
```

GENERICS make identifying bugs/code breaks faster throughout lifecycle (preferably before prod runtime & in compile time) and subsequently cheaper to fix due to less resources being exhausted

```

interface ISports {
    String getName();
}

abstract class Player implements ISports {

    private final String name;

    public Player(String name) {
        this.name = name;
    }

    @Override
    public String getName() {
        return this.name;
    }
}

class FootballPlayer extends Player {

    public FootballPlayer(String name) {
        super(name);
    }
}

// Comparable<Team<T>> = only compare the same-sport teams
class SportsTeam<T extends Player> implements Comparable<SportsTeam<T>> {

    private final String ALREADY_ON_TEAM = " already on team";
    private final String ADDED_TO_TEAM = " added to team";

    private String name;
    private int won;
    private int tied;

    // GENERICS: specify datatype parameters when creating classes, interfaces, or methods thus improving ENCAPSULATION
    private ArrayList<T> members;

    public SportsTeam(String name) {
        this.name = name;

        this.members = new ArrayList<T>();
        this.won = 0;
        this.tied = 0;
    }

    public boolean addPlayer(T player) {

        if(this.members.contains(player)) {

            // since using GENERICS CLASS extends bound Type parameter, no need to cast dataType
            System.out.println(player.getName() + ALREADY_ON_TEAM);
            return false;
        }

        this.members.add(player);
        System.out.println(player.getName() + ADDED_TO_TEAM + " " + this.getName());

        return true;
    }

    public int ranking() {
        return (this.won * 2) + this.tied;
    }

    @Override
    public int compareTo(SportsTeam<T> team) {

        boolean isLowerRank = (this.ranking() > team.ranking());
        boolean isHigherRank = (this.ranking() < team.ranking());
        int sameRank = 0;

        if(isLowerRank) {
            return -1;
        } else if(isHigherRank){
            return 1;
        }
        return sameRank;
    }

    public String getName() {
        return name;
    }
}
```

# Concurrency

software that can execute processes simultaneously (one task doesn't have to complete before another one can start)

__CONCURRENCY BENEFITS__

- free up the main thread so that it can continue working and executing, you can report progress or accept user input and perform those other tasks on the screen or in other parts of the program, while another long-running task that we kicked off in another thread continues to execute in the background.

- might want to use threads is because an API requires us to provide one.

__PROCESS__

an instance of a computer program with its own memory space that's sequentially executed by a computer system that has the ability to run several computer programs concurrently.

- every process has a memory HEAP 

```
java virtual machine instance ->
        the JVM runs as a PROCESS ->
            running a java console application ->
                we're initiating said PROCESS
```

__THREAD__

a unit of execution within a process, each process can have multiple threads: a method for a program to "split" itself into two or more simultaneously or pseudo-simultaneously running tasks.

- every thread has a memory THREAD STACK.

```
// THREADS .start(): only JVM executes .run() for a given single Thread (always a new Thread instance), including priority-assigned threads, and CANNOT assume Thread instance execution order
new Thread() {
    @Override
    public void run() {
        System.out.println("Hello from anonymous class Thread")
    }
}.start();
```

__MULTITHREADING__

the JVM is multi-processed and multithreaded and has background processes running while a single-thread (main) process/application is executing.

__THREAD JOIN__

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

the process of semi-controlling/influencing when threads execute code and therefore when they can access the heap is called synchronization.

- when working with threads, we have to synchronize all areas where we think or where interference can happen.

__THREAD SYNCHRONIZATION code blocks__

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

__DEAD LOCKS__

application freezes during execution due to unreleased INTRINSIC LOCKS - the synchronized shared-resource code executes one at a time and the single running thread is holding the objects INTRINSIC LOCK blocking other threads that WAIT for the lock release via NOTIFY

__THREAD SYNCHRONIZATION + DEADLOCKS__

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

__ARRAY BLOCKING QUEUE__

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

__EXECUTOR SERVICE__

optimize a managed set of threads, thus reducing the overhead of thread creation

```
int numThreads = 3;
ExecutorService executorService = Executors.newFixedThreadPool(numThreads);

executorService.execute(producer);
executorService.execute(consumer1);
executorService.execute(consumer2);
```

__FUTURE__

a return value from an executed thread in a thread pool

```
// THREADS + ANONYMOUS CLASSES/LAMBDA: when using anonymous classes, immediately executing no-name Thread class w/ Thread.subclass parameter that implements Runnable interface to .start() on its own thread in the HEAP
Future<String> future = executorService.submit(new Callable<String>() {
    @Override
    public String call() throws Exception {
        return "executorService.submit() was called; this is the result";
    }
});
```

__ATOMIC ACTIONS__

once a thread starts these actions, they cannot be suspended during execution, and must complete

- reading and writing reference variables

- reading and writing primitive variables, exception long & double

- reading and writing volatile variables

```
int atomicAction1 = 1;
int atomicAction2 = atomicAction1;
```

__VOLATILE VARIABLES__

the JVM writes the value back to main memory immediately after a thread updates the value in its CPU cache, and it also guarantees that every time a variable reads from a volatile variable, it will get the latest value.

```
public volatile int volatileVariable;
```

__THREAD STARVATION__

threads aren't given the opportunity to progress due to threat priority - assigning a high priority to a thread means the OS should try and run the thread before other waiting threads.


# Data Structures

# arrays

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

# vectors

VECTORS are thread-safe ArrayList: if 1 or more threads are writing (CRUD) to an ArrayList there could be thread conflicts

- thread-safe: no conflict when using on different threads with manually having to synchronize the code (synchronization has overhead performance issue)

```
List<Employee> employeeList = new Vector<>();
```

Vector.add(value) = SYNCHRONIZED add given value to vector

```
employeeList.add(new Employee("First 1", "Last 1", 124));
employeeList.add(new Employee("First 2", "Last 2", 22));
```

# sets

sets are a computationally fast unordered collection WITHOUT DUPLICATES implemented via a HASHSET class

```
Set<Integer> numbers = new HashSet<>();
numbers.add(1);
```

__SET UNION__

a set (WITHOUT DUPLICATES) that contains ALL elements of 2 or more hashsets via hashSet.addAll()

```
Set<Integer> set1 = new HashSet<>();
Set<Integer> set2 = new HashSet<>();

set1.addAll(set2);
```

.EQUALS & .HASHCODE @Override both methods if using own object as map key or set element

- HASHSET element/ HASHMAP key custom CLASSES: @Override .equals() & .hashcode() methods - if 2 objects compare equal, then they must have same collection bucket hashcode

__VENN DIAGRAM ASYMMETRIC DIFF__

remove all shared elements of 1 set found in another set via bulk operation hashSet.removeAll()

```
Set<Integer> set1 = new HashSet<>();
Set<Integer> set2 = new HashSet<>();

set1.addAll(set2);

Set<Integer> asymmetric = new HashSet<>(set1);
asymmetric.removeAll(set2);
```

__VENN DIAGRAM SYMMETRIC DIFF__

remove all shared elements found in both sets & return all non-shared elements of both sets (hashSetUnion - hashSetIntersection)

# Singly LinkedLists

HEAD --> { currentNodeValue, nextNodePointer } --> { currentNodeValue, nextNodePointer } --> null

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

    // OOP GETTERS & SETTERS
}
```

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
        EmployeeNode newNode = new EmployeeNode(employee);

        // set the current head as the new node's next value (shift current head down 1 node)
        newNode.setNext(this.head);

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

    // OOP GETTERS & SETTERS
}
```

# Doubly LinkedLists

null --> HEAD <--> {previousPointer, currentNodeValue, nextNodePointer } <--> {previousPointer, currentNodeValue, nextNodePointer } <--> TAIL --> null

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

    // OOP GETTERS & SETTERS
}
```

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

        if(this.isEmpty()) {

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

        if(this.isEmpty()) {

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

        if(this.isEmpty()) return null;

        EmployeeNode removedNode = this.head;

        boolean hasOnlyOneNode = (this.head.getNext() == null);

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

        if(this.isEmpty()) return null;

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

    // OOP GETTERS & SETTERS
}
```

# Stacks

LIFO STACKS: an abstract class that only accesses variables from the top/front on a stack because it's a last-in, first-out (LIFO) data structure implemented by a LINKED_LIST or ARRAY

- LINKED_LIST STACK O(1) constant TIME COMPLEXITY: due to LIFO (only accessed from the top/front), for push(), pop(), peek()

- ARRAY STACK O(n) linear TIME COMPLEXITY: due to LIFO (only accessed from the top/front), for push(), pop(), peek()

```
public class ArrayStack {

    // STACK top: always null because it's a placeholder for next potential item; actual top of stack is the last index of the array
    private int top;
    private Employee[] stack;

    public ArrayStack(int capacity) {
        this.stack = new Array[capacity]
        this.top = 0;
    }

    public boolean isEmpty() {
        return this.top == 0;
    }

    /**
     * get object at top/front of stack but do not remove
     */
    public Employee peak() {

        if(this.isEmpty()) throw new EmptyStackException();

        int firstIndex = this.top - 1;
        return this.stack[firstIndex];
    }

    public void push() {

        boolean isFullForResize = (this.top == this.stack.length);

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

        if(this.isEmpty()) throw new EmptyStackException();

        // STACK top: the actual top of stack is the last index of the array
        int indexLIFO = --this.top;
        Employee poppedEmployee = this.stack[indexLIFO];

        // STACK top is always null because it's a placeholder for next potential item
        this.stack[this.top] = null;

        return poppedEmployee;
    }

    public Employee[] getStack() {

        for(int i = 0; i < this.stack.length; i++) {
            System.out.println(this.stack[i]);
        }
        return this.stack;
    }
}
```

# Maps

an INTERFACE of unique_key-value pairs implemented by the HASHMAP or LINKED HASHMAP classes with 2 GENERIC parameters

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

FIFO QUEUES: an abstract class that only accesses variables from the top/front on the queue because it's a first-in, first-out (FIFO) data structure implemented by a LINKED_LIST or ARRAY

- ARRAY QUEUES O(n) linear TIME COMPLEXITY: due to FIFO (only accessed from the top/front), for add(), pop(), peek()

- LINKED_LIST QUEUES O(1) constant TIME COMPLEXITY: due to FIFO (only accessed from the top/front), for add(), pop(), peek()

CIRCULAR QUEUE: wrap queue back-to-front, where back field is always pointing to next available queue position

```
public class CircularQueue {

    private Employee[] queue;
    private int front;
    private int back;

    public CircularQueue(int capacity) {
        this.queue = new Employee[capacity]
        this.front = 0;
        this.back = 0;
    }

    public int getSize() {

        boolean isWrapped = (this.front <= this.back);
        int wrappedSize = this.back - this.front;

        if(isWrappedQueue) return wrappedSize;

        // to handle negative number when wrapped circular queue size, wrapped queue numElements is add queueLength to wrappedSize
        return (wrappedSize + this.queue.length);
    }

    public boolean isEmpty() {
        return this.getSize() == 0;
    }

    /**
     * O(1) constant time complexity: preview only first item at the front of the queue
     */
    public Employee peek() {

        if(this.isEmpty()) return throw new NoSuchElementException();

        return this.queue[this.front];
    }

    /**
     * O(1) constant time complexity: adding to a full circular queue needs to be resized/doubled
     */
    public void push(Employee employee) {

        if(employee == null) return;

        int lastIndex = this.queue.length - 1;
        boolean isFullAndResize = (this.getSize() == lastIndex);

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
        boolean isWrapped = (this.back <= lastQueueIndex);

        this.back = isWrapped ? this.back + 1 : 0;
    }

    /**
     * O(1) constant time complexity: remove first item that is at the front of the queue
     */
    public Employee pop() {

        if(this.isEmpty()) throw new NoSuchElementException();

        // FIFO: get employee at the front of the queue
        Employee employee = this.queue

        // null-out first index and move queue front index up by 1
        this.queue[this.front] = null;
        this.front++;

        boolean isFullyWrapped = (this.front == this.queue.length);

        // if queue is empty after removal of front: reset queue
        if(this.isEmpty()) {

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
public class BinaryTree {

    private static final String EMPTY_TREE = "This binary tree is empty";
    private static final String IN_ORDER_TRAVERSAL = "In-order Traversal";

    private TreeNode root;

    public BinaryTree() {
        this.root = null;
    }

    public boolean isEmpty() {
        return this.root == null;
    }

    public void traverseInOrder() {

        if(this.isEmpty()) return;

        System.out.println(IN_ORDER_TRAVERSAL);
        this.root.traverseInOrder();
    }

    public void insertNode(int value) {
        if(this.isEmpty()) {
            this.root = new TreeNode(value);
        } else {
            this.root.insertNode(value);
        }
    }

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
        if(this.isEmpty()) {
            System.out.println(EMPTY_TREE);
            return Integer.MIN_VALUE;
        } else {
            return this.root.getMin();
        }
    }

    public int getMax() {
        if(this.isEmpty()) {
            System.out.println(EMPTY_TREE);
            return Integer.MIN_VALUE;
        } else {
            return this.root.getMax();
        }
    }

    public TreeNode getNode(int value) {

        if(this.isEmpty()) return null;

        return this.root.getNode(value);
    }

    // OOP GETTERS & SETTERS

    // INNER CLASS: logically grouped components within an extending parent super class
    protected class TreeNode {

        private int data;
        private TreeNode leftChild;
        private TreeNode rightChild;

        public TreeNode(int data) {
            this.data = data;
        }

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

            if(isBaseCase) return this.data;

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

            if(isBaseCase) return this.data;

            // ! RECURSION: continuously self-calling algorithm & each call waits for a return value until reaching a base case or experiences a stack overflow
            return this.rightChild.getMax();
        }

        // OOP GETTERS & SETTERS
    }
}
```

# Heaps

```
public class Heap {

    private static final String HEAP_FULL = "Heap is full";
    private static final String HEAP_EMPTY = "Heap is empty";

    private int[] heap;
    private int size;

    public Heap(int capacity) {
        this.heap = new int[capacity];
    }

    public boolean isEmpty() {
        return this.size == 0;
    }

    public boolean isFull() {
        return this.size == this.heap.length;
    }

    public int getParent(int index) {
        return (index - 1) / 2;
    }

    public int getChild(int parentIndex, boolean isLeftChild) {

        int currentChild = isLeftChild ? 1 : 2;
        return (2 * parentIndex) + currentChild;
    }

    public void printHeap() {

        for(int i = 0; i < this.size; i++) {
            System.out.print(this.heap[i] + ", ");
        }
    }

    public void sort() {

        if(this.isEmpty()) return;

        int lastHeapIndex = this.size - 1;

        for(int i = 0; i < lastHeapIndex; i++) {

            // the root = largest value in heap
            int tempRoot = this.heap[0];

            // swap root for last node in heap
            this.heap[0] = this.heap[lastHeapIndex - 1];
            this.heap[lastHeapIndex - i] = tempRoot;

            // heapify() & reduce heap by 1 (exclude swapped value) on every root-last index swap
            int adjustedLastIndex = (lastHeapIndex - i) - 1;
            fixHeapBelow(0, adjustedLastIndex);
        }
    }

    public int peek() {

        if(this.isEmpty()) throw new IndexOutOfBoundsException(HEAP_EMPTY);

        int root = this.heap[0];
        return root; 
    }

    public void insert(int value) {

        if(this.isFull()) throw new IndexOutOfBoundsException(HEAP_FULL);

        this.heap[this.size] = value;

        // pass index where we have placed the newValue
        fixHeapAbove(this.size);
        this.size++;
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

__BUBBLE SORT:__

```
[[unsortedPartition][]] -> [[unsortedPartition][sortedPartition]] -> [[][sortedPartition]]
```

TIME COMPLEXITY O(n-squared) = worst performing nested loops, each loop corresponds to n in Big-O notation, thus O(n^2)

SPACE COMPLEXITY: in-place algorithm that doesn't use extra memory

STABLE ALGORITHM: if there are duplicate elements, the original order of these elements will be preserved

- only swap if i > (i + 1)

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

__SELECTION SORT:__

```
[[unsortedPartition][]] -> [[unsortedPartition][sortedPartition]] -> [[][sortedPartition]]
```

TIME COMPLEXITY O(n-squared) = worst performing nested loops, each loop corresponds to n in Big-O notation, thus O(n^2)

SPACE COMPLEXITY: in-place algorithm that doesn't use extra memory

STABLE ALGORITHM: if there are duplicate elements, the original order of these elements will be preserved

- only swap if i > (i + 1)

SELECTION SORT LOGIC:

selection sort breaks the array into 2 partitions:

- sorted and unsorted: the arrays starts unsorted & unsorted partition shrinks from left to right

```
[[unsortedPartition][]] -> [[unsortedPartition][sortedPartition]] -> [[][sortedPartition]]
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

            boolean foundLargerUnsortedElement = (array[currentLargestIndex] < array[index]);

            if(foundLargerUnsortedElement) {
                currentLargestIndex = index;
            }
        } else { // reached unsortedPartition end

            boolean hasLargerLastUnsorted = (array[currentLargestIndex] < array[lastUnsortedIndex]);
            if(hasLargerLastUnsorted) {

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

__INSERTION SORT:__

```
[[][unsortedPartition]] -> [[sortedPartition][unsortedPartition]] -> [[sortedPartition][]]
```

TIME COMPLEXITY O(n-squared) = worst performing nested loops, each loop corresponds to n in Big-O notation, thus O(n^2)

SPACE COMPLEXITY: in-place algorithm that doesn't use extra memory

STABLE ALGORITHM: if there are duplicate elements, the original order of these elements will be preserved

- only swap if i > (i + 1)

LOGIC:

STEP 1) insertion sort breaks the array into 2 partitions: sorted and unsorted

- sorted partition starts as a 1 element array (index 0)

- unsorted partition starting at index 1

STEP 2) the inserting of the UNSORTED_PARTITION_VALUE is done in the SORTED partition where there is no swapping, the elements shift

- on 1st iteration, take first element in the unsorted partition (index 1)

- save unsorted inserting value since shifting of elements might cause overwritten value

- then "insert" it into the sorted partition by comparing if it is greater than or equal to the value in the sorted partition

    - if sorted partition value is less than or equal to the unsorted inserting value,
        than the inserting value is inserted at the index above the sorted partition value

    - if the sorted partition value is greater than the unsorted inserting value,
        than you shift the sorted partition value up 1
        next, compare unsorted inserting value to the next decremented index value

    - repeat this process until you find the correct index for the unsorted inserting value, or you reach the beginning of the array (index 0)

STEP 3) after the comparison(s) & inserting of the unsorted inserting value

- GAP VALUE 1 = the sorted partition is grown by 1 and the index in the unsorted partition is incremented by 1

STEP 4) repeat this process until the entire array is sorted

```
public static void insertionSort(int[] array) {

    int insertValue;

    // outer FOR_LOOP is growing UNSORTED_PARTITION by 1 after inserting it's values into SORTED_PARTITION
    // sorted partition starts with index 0; unsorted partition starts with index 1 as it's first element
    for(int unsortedIndex = 1; unsortedIndex < array.length; unsortedIndex++) {

        // save unsorted inserting value since shifting of elements might cause overwritten value
        insertValue = array[unsortedIndex];

        // traverse sorted partition for correct index of insertValue
        // while not at beginning of partition AND (sortedPartitionElement is greater than unsorted insertElement)
        for(int i = unsortedIndex; (i > 0) && (array[i - 1] > insertValue); i--) {

            // if unsortedPartition insertValue less than currentSortedValue, shift left-to-right currentSortedValue up
            int sortedPartitionElement = array[i - 1];

            // shift left-to-right currentSortedValue up
            array[i] = sortedPartitionElement;
        }

        // on finding correct index, assign unsorted insertValue to index in sorted partition
        array[i] = insertValue;

        // outer FOR_LOOP is growing both partitions by 1 after inserting UNSORTED_PARTITION_ELEMENT into SORTED_PARTITION
    }
}
```

__SHELL SORT:__

SHELL SORT is a VARIATION of INSERTION SORT

```
[[][unsortedPartition]] -> [[sortedPartition][unsortedPartition]] -> [[sortedPartition][]]
```

Big(O) TIME COMPLEXITY: the varying gap value you decide on influences the time complexity for shell sort

SPACE COMPLEXITY: in-place algorithm that doesn't use extra memory

UNSTABLE ALGORITHM: if there are duplicate elements, the original order of these elements will NOT always be preserved

SHELL SORT LOGIC:

- PRELIMINARY WORK

    - if majority array is mostly in correct order, no need to shift every element like insertion sort

    - do preliminary work by starting with large gap value that gradually decreases with each iteration & shift elements (no swapping)

        - shell sort uses larger than 1 gapValue unlike insertion sort which has gapValue of 1

        - after initial iteration w/ large gap value, increment index of both gapValue and compValue & repeat until gapValue index is greater than array length

        - compare array[j-gapValue] with insertingElement

- INSERTION SORT

    - on the last iteration, when the gap value is 1

    - the array has been partially sorted and no longer requires extensive shifting,

    - then insertion sort is applied

GAP VALUE STRATEGY POPULAR: Knuth Sequence

GAP VALUE STRATEGY EXAMPLE:

- gap value is calculated using array's length:

```
int gapValue = array.length / 2
```

- on each iteration, we will divide the gap value by 2 to get the next gap value

- for the array below, there will only be 2 iterations

```
[20,35,-15,7,55,1,-22]

// the (i) initialized gapValue = 3
// the (j) sorted partitionValue = i = 3
// gap value = array.length / 2
// unsortedPreliminaryElement = array[gapValue]
```

- compare array[j-gapValue] against unsortedPreliminaryElement

- once you reach the end of the array on the 1st iteration, compare the first element again using the gap value
- on the next/last iteration, the gapValue will be 1 for this array
- if the gapValue is 1, then execute insertion sort

```
public static void shellSort(int[] array) {

    int insertValue;

    /*
        PRELIMINARY WORK

            [20,35,-15,7,55,1,-22]

        gap = midpoint index of array (7 at index 3)
        continue loop while gap is greater than 0
        after each iteration divide gap by 2
     */
    for(int gap = (array.length / 2); gap > 0; gap /= 2) {

        for(int i = gap; i < array.length; i++) {

            // save unsorted inserting value since shifting of elements might cause overwritten value
            insertValue = array[i];

            // use j to traverse sorted partition
            int j = i;

            // if index j is less than gap, reached front of array/sortedPartition
            while((j >= gap) && (array[j - gap] > insertValue)) {

                array[j] = array[j - gap];

                // decrement to repeat until reaching the beginning of the array/sortedPartition
                j -= gap;

                // INSERTION SORT when gap = 1
            }
            // shift insertingValue to approximated correct index
            array[j] = insertValue;
        }
    }
}
```

__MERGE SORT:__

Big(O) LOGARITHMIC TIME COMPLEXITY = O(logn) = O of log to the base 2 n

- repeatedly dividing array in half during splitting

SPACE COMPLEXITY NOT in-place

- splitting phase = in-place algorithm that doesn't use extra memory
    - track splitting via indices

- merge phase = NOT in-place algorithm
    - creates temporary arrays for sorting siblings for merge

STABLE ALGORITHM: if there are duplicate elements, the original order of these elements will be preserved

- only swap if index_i > (index_i + 1)

MERGE SORT LOGIC:

- divide & conquer algorithm:

    - splitting base problem into several mini-problems, solving mini-problems, and then merging mini-solutions to solve base problem

- recursive algorithm:

    - calls itself until reaching a base case and then feeds return values to itself to solve backwards

PHASE 1: logical splitting (in-place = no new arrays)

- divide the array into two sub-arrays (left & right partition)
- then recursively divide each subsequent array into two arrays
- UNTIL you have multiple sorted arrays of 1 length

```
split left side first, then right side last
    each split results in 'sibling arrays'

      EXAMPLE:

                   [20, 35, -15, 7, 55, 1, -22]

          [20, 35, -15]       &&            [7, 55, 1, -22]

      [20]    &&  [35, -15]            [7, 55]    &&      [1, -22]

                 [35] && [-15]       [7] && [55]        [1] && [-22]
```


PHASE 2: not in-place merging, sorting elements starting from bottom-to-top with temporary array

- handle left side first, then right side, merge all sibling arrays on left & right side before proceeding to higher level to recursively merge resulting sibling arrays

STEPS:

- create temp array that can hold all elements in the arrays we're merging

- set i to 1st index of left sibling array

- set j to 1st index of right sibling array

- traverse through left & right array & get the smallest value for temp: compare left[i] to right[j] sibling arrays

    - if left[i] is smaller, copy to temp array and increment i by 1
    - if right[j] is smaller, copy to temp array and increment j by 1

    repeat until temp array has merged all elements into temp array in sorted order

- copy temp array back into original input array at the correct position (making it a STABLE algorithm)

- repeat steps 4 & 5 until you have sorted original input array

```
public class MergeSort {

    private static int[] array = {20, 35, -15, 7, 55, 1, -22};

    public static int[] execute() {
        recursivePartition(array, 0, array.length);
        return array;
    }

    // RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)
    private static void recursivePartition(int[] array, int start, int end) {

        // RECURSIVE BASE CASE: the breaking condition that initiates an upward propagation of return of values for the waiting calls that results in a call-stack resolution or overflow
        int partitionLength = end - start;
        boolean isBaseCase = (partitionLength < 2);

        if(isBaseCase) return;

        // RECURSION + DIVIDE & CONQUER: partition LEFT side FIRST, then RIGHT side with midpoint via start & end indices 
        int midpoint = (start + end) / 2;

        // LEFT partitions
        // [20, 35, -15] ->
        //      [20] [35, -15] ->
        //          [20] [35] [-15]

        recursivePartition(array, start, midpoint);

        // RIGHT partitions 
        // [7, 55, 1, -22] ->
        //      [7, 55] [1,-22] ->
        //          [7] [55] [1] [-22]

        recursivePartition(inputArray, midpoint, end);

        // merging left & right RECURSIVE partitions returns arrays w/ sorted elements
        merge(array, start, midpoint, end);
    }

    private static void merge(int[] array, int start, int midpoint, int end) {

        int leftPartitionEnd = array[midpoint - 1];
        int leftPartitionStart = array[midpoint];

        boolean isAlreadySorted = (leftPartition <= rightPartitionStart);

        if(isAlreadySorted) return;

        int i = start;
        int j = midpoint;
        int tempIndex = 0;

        int tempLength = end - start;
        int tempArray = new int[tempLength];

        // isTraversingLeft = (i < midpoint);
        // isTraversingRight = (j < end);

        while(i < midpoint && j < end) {

            // preserve partition bounds
            int currentLeftElement = array[i];
            int currentRightElement = array[j];

            // MERGE SORT: write smaller of 2 comparison elements to temp array for left-to-right sorted order
            // STABLE ALGORITHM: if equal, write left first to preserve original order

            tempArray[tempIndex++] = (currentLeftElement <= currentRightElement) ? inputArray[i++] : inputArray[j++];
        }

        /*
            MERGE SORT OPTIMIZATION

                LEFT partition remaining elements, must copy to temp array

                RIGHT partition remaining elements, no copying into temp array needed bc already will be in sorted order for input array
         */

        int[] srcArray;
        int destinationIndex = start + tempIndex;
        int remainingElementIndex = i;

        // no action, if no remainder left partition elements, else move to correct index
        int notCopiedCount = midpoint - i;

        // copying sorted tempArray elements back into inputArray
        srcArray = array;
        System.arraycopy(srcArray, remainingElementIndex, array, destinationIndex, notCopiedCount);

        // only copy numElements in tempArray into array
        srcArray = tempArray;
        System.arraycopy(srcArray, 0, array, start, tempIndex);
    }
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
