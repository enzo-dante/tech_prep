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

# Java Keywords

__CONSTANTS__

static class variables assigned FINAL value before compilation/instantiation

```
private static final String POWER_USER = "I am a power user";
```

__ACCESS-MODIFIERS__

control the access to a given variable or method with a keyword

```
public class Person {

    // PRIVATE keyword: access to the variable or method is limited to the scope of the defining class
    private String name;

    // PUBLIC keyword: the variable or method can be accessed from any scope
    public Person(String name) {
        this.name = name;
    }

    // PROTECTED keyword: access to the variable or method is limited to the scope of the defining class & it's INHERITED subclasses within the package
    protected String talk() {
        return "This is protected speech";
    }
}
```

__STATIC__

a unique class variable assigned to a single space in memory & referenced across an entire application

```
public class Test {

    private static final String NAME = "My name";

    public static void sayMyName() {
        System.out.println(NAME);
    }
}
```

__STATIC INITIALIZATION BLOCKS__

one-time on-initialization execution of the 'static {}' and their assigned STATIC FINAL variables

```
private static final String OWNER;
private static final String FIRST_STATIC_MSG;

static {
    OWNER = "Tim";
    FIRST_STATIC_MSG = "The owner is " + OWNER;
    System.out.println(FIRST_STATIC_MSG);
}
```

__METHOD OVERLOADING__

use the same name, but with unique parameters, for related methods to reduce tech debt and optimize readability & scalability

```
// method 1
public int add() {
    return 1 + 1;
}

// method 2
public int add(int a, int b) {
    return a + b;
}

// method 3
public int add(int n, String msg) {
    System.out.println(msg);
    return 100 + n;
}
```

__AUTOBOXING__

converting a primitive dataType variable -> a corresponding Wrapper class dataType variable with greater functionality

```
int primitiveIntVariable = 1;
Integer wrappedInteger = primitiveIntVariable;
```

__UNBOXING__

casting a Wrapper class dataType variable with greater functionality -> corresponding primitive dataType variable

```
private static double calculateInterest(Double amount, Double interestRate) {
    return amount * (interestRate/100);
}
```

__ternary operator__

a ternary operator is shorthand for a simple if-else statement

```
String currentName = (hunger > 70) ? "Can't remember" : "Bill";
```

__WRAPPER CLASS__

class dataType variables with greater functionality

```
int currentValue = Integer.parseInt(numberSubstring);
```

__Ojbect-Oriented Programming (OOP) CLASSES__

Classes are used to create and manage new objects and support inheritance (a key ingredient in object-oriented programming and a mechanism of reusing code).

A class' state may be comprised of class fields (the object attributes) and methods (the object's callable implementations of behavior)

On object instantiation, the object's initial state might need to be set by providing initial values for the class instance.

```
public class Animal {

    // CONSTANTS/static class variables assigned FINAL value before compilation/instantiation
    private static final String SLEEPING = " goes to sleep.";

    // OOP ENCAPSULATION private class fields
    private int energy;
    private boolean isHungry;
    private String name;
    private int numLegs;

    // OOP CONSTRUCTOR method that initializes the class fields & INTRINSIC LOCK on the instantiation of the class/object blueprint
    public Animal(int numLegs, int energy) {

        this.numLegs = numLegs;
        this.energy = energy;

        // default value
        this.name = "unnamed".toUpperCase();
        this.isHungry = false;
    }

    // CLASS METHODS: unique object behavior
    public void sleep() {

        System.out.println(this.name + SLEEPING);
        this.energy = 100;

        this.toggleHunger();
    }

    private void toggleHunger() {
        this.isHungry = !this.isHungry;
    }

    // OOP GETTERS & SETTERS
    public boolean isHungry() {
        return this.isHungry;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getNumLegs() {
        return this.numLegs;
    }

    public int getEnergy() {
        return this.energy;
    }

    public void setEnergy(int energy) {
        this.energy = energy;
    }
}
```

__OOP CLASS INSTANCES__

An instance is a specific object created from a specific class blueprint.

```
// The user-defined objects are created using the class keyword.
public static void main(String[] args) {

    Animal animal = new Animal(4);

    animal.setName("Toby the Dog");
    System.out.println(animal.getName() + " has " + animal.getNumLegs() + " legs.");
}
```

```
Scanner scanner = new Scanner(System.in);
scanner.close();
```

__OOP COMPOSITION + INNER CLASS__

logically grouped class components within an extending parent super class

```
public class PC {

    // OOP ENCAPSULATION private class fields
    private Motherboard motherboard;

    // OOP CONSTRUCTOR that initializes the class fields on class/object instantiation
    public PC(int ramSlots) {
        this.motherboard = new MotherBoard(ramSlots);
    }

    // OOP GETTERS & SETTERS methods
    public Motherboard getMotherboard() {
        return this.motherboard;
    }

    // inner class
    protected class Motherboard {

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

    final String PLAY_DECLARATION = "I play sports";
}

public class Player implements ISports {

    private final String name;

    public Player(String name) {
        this.name = name;
    }

    @Override
    public void play() {
        System.out.println(PLAY_DECLARATION);
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

} catch(ExecutionException e1) {

    System.out.println(e1.getMessage());

} catch(InterruptedException  e2) {

    System.out.println("Thread running the task was interrupted");
}
```

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

  - you CANNOT instantiate an ABSTRACT CLASS, must use a normal class that inherits from ABSTRACT CLASS for instantiation

__OOP INHERITANCE__

child subclass inherits public class fields + methods from extending parent super class

abstract keyword = no logic in the given code block, only define the class or method signature shared across adhering classes that will be implemented later by inheriting subclasses.

```
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

ABSTRACT CLASSES can have class fields/object instance members AND define abstract publicly-shared signatures

- you CANNOT instantiate an ABSTRACT CLASS, you must use a normal class that inherits from an ABSTRACT CLASS for instantiation

INTERFACES can ONLY define publicly-shared signatures & public CONSTANTS

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

    // Getters & Setters
}
```

# Recursive Functions

a continuously self-calling algorithm & each call on the call-stack waits for the algorithm to reach a base case/breaking condition for a return value.

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

__RECURSIVE BASE CASE__

the breaking condition that initiates an upward propagation of return of values for the waiting calls that results in a call-stack resolution or overflow

```
private static int recursiveFactorial(int number) {

    boolean isBaseCase = (number == 0);

    if(isBaseCase) return 1;

    int decrementedNumber = number - 1;

    return recursiveFactorial(decrementedNumber) * number;
}
```

# Divide & Conquer

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

    // RECURSION: a continuously self-calling algorithm & each call on the call-stack waits for the algorithm to reach a base case/breaking condition for a return value.
    private static void recursivePartition(int[] array, int start, int end) {

        // RECURSIVE BASE CASE: the breaking condition that initiates an upward propagation of return of values for the waiting calls that results in a call-stack resolution or overflow
        int partitionLength = end - start;
        boolean isBaseCase = (partitionLength < 2);

        if(isBaseCase) return;

        int midpoint = (start + end) / 2;

        // RECURSION + DIVIDE & CONQUER: partition LEFT side FIRST w/ midpoint via start & end indices
        // [20, 35, -15] ->
        //      [20] [35, -15] ->
        //          [20] [35] [-15]

        recursivePartition(array, start, midpoint);

        // RECURSION + DIVIDE & CONQUER: then RIGHT side with midpoint via start & end indices
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

            tempArray[tempIndex++] = (currentLeftElement <= currentRightElement) ? array[i++] : array[j++];
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

- MEMOIZATION is a technique that can be used to improve the efficiency of divide & conquer algorithms by storing the solutions to earlier problems & eliminating redundant calls

# Data Structures

# Arrays

<img src="/content/ds_array.png">

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

# 2D Arrays / Matrix

<img src="/content/ds_matrix.png" alt="data structure 2-dimensional array">

Two Dimensional arrays are needed when data is formatted as TABLE or SPREADSHEET

```
Example:
    movie ratings by multiple reviewers
        Each row is a different reviewer
        Each column is a different movie

        ratings = [
            [4,6,2,5],
            [7,9,4,8],
            [6,9,3,7]
        ];

        ratings[1][3] = 8
            [1] = row
            [3] = column
```

```
public class AmazonProblem {

    public static void main(String[] args) {

        // the minefield is a 2D array
        int[][] mineField = {
                {0,1,0,1},
                {0,1,1,1},
                {0,0,0,0},
                {0,1,0,0}
        };

        int numMineClusters1 = getMineClusterCount(mineField);
        System.out.println("\nNESTED FOR LOOPS total: " + numMineClusters1 + " mine clusters.");

        int[][] mineField2 = {
                {0,1,0,1},
                {0,1,1,1},
                {0,0,0,0},
                {0,1,0,0}
        };
    }

    private static int getMineClusterCount(int[][] array2D) {
        /*
            identify 2 separate mine clusters in a 4x4 grid below
                that uses nested loops and the divide and conquer method
                the method should return 2 since there are 2 separate clusters
                identify the time complexity

            the 4x4 mine grid:
                0 - no mine
                1 - mine
                    [[0,1,0,1],
                    [0,1,1,1],
                    [0,0,0,0],
                    [0,1,0,0]]
         */

        System.out.println("\n\tgetMineClusterCount()\n");
        int numClusters = 0;

        // time complexity of O(n^2) quadratic time complexity given nested for loops
        for(int i = 0; i < array2D.length; i++) {

            for(int column = 0; column < array2D[i].length; column++) {

                int[] row = array2D[i];
                int columnValue = row[column];

                // as soon as you find the first cluster of mines
                if(columnValue == 1) {

                    numClusters++;
                    System.out.println("found a cluster".toUpperCase());
                    array2D = zeroOutMineCluster(array2D, i);
                }
            }
        }
    }

    private static int[][] zeroOutMineCluster(int[][] array2D, int rowIndex) {

        int[] zeroRow = {0,0,0,0};

        int adjacentRowIndex = rowIndex + 1;
        array2D[rowIndex] = zeroRow;

        // validate against out-of-bounds exception
        if(adjacentRowIndex < array2D.length) {

            // since clusters are separate you can zero out the adjacent row without fear of removing an unaccounted cluster
            array2D[adjacentRowIndex] = zeroRow;
        }

        return array2D;
    }
}
```


# Vectors

VECTORS are thread-safe ArrayLists: if 1 or more threads are writing (CRUD: CREATE, READ, UPDATE, DELETE) to an ArrayList there could be thread conflicts

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

<img src="/content/ds_hashtable.png" alt="data structure set">

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

<img src="/content/ds_singly_linked_list.png" alt="data structure singly linked list">

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
// Singly LinkedLists w/ an array backing
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
        this.head = newNode;

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

<img src="/content/ds_doubly_linked_list.png" alt="data structure doubly linked-list">

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
// Doubly LinkedLists w/ an array backing
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

<img src="/content/ds_stack.png" alt="data structure stack">

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

<img src="/content/ds_hashtable.png" alt="data structure maps">

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

<img src="/content/ds_queue.png" alt="data structure queue">

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

<img src="/content/ds_tree.png" alt="data structure tree">

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

<img src="/content/ds_heaps.png" alt="data structure heaps">

a complete binary tree with array-backing, only interested in  min & max at ROOT of tree O(1) time complexity that functions left-to-right

- O(1) CONSTANT time complexity:

    - insert

    - remove/poll

    - peak/getRoot

__HEAPIFY__

the process of converting a binary tree into a heap after inserting or deleting a node

__JAVA PRIORITY QUEUE MIN HEAP__

a MIN HEAP where every parent has to have a value that is less than or equal to its children in a complete binary tree (lower the number, the higher the priority)

- Traveling from the root down to the leaves, all the paths would be in ascending order

- if you start at a leaf and travel up to the root, all the paths would be in descending order

__PRIORITY QUEUES MAX HEAPS__

every parent has to have a value greater than or equal to its children in a complete binary tree

- Traversing down to every leaf, all the values along each path should be in descending order.

```
MAX HEAP
                 22

            19       18

    15     3             14     4

12
```

a MAX HEAP implementation w/ array backing always want the highest priority item first

- for MAX HEAPS, a comparator is required that will look at the two values and whenever you have one value greater than the other you in fact want to return that that value's less.

```
public class MaxHeap {

    private static final String HEAP_FULL = "Heap is full";
    private static final String HEAP_EMPTY = "Heap is empty";

    private int[] heap;
    private int size;

    public MaxHeap(int capacity) {
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

    /*
        MAX HEAP sort():

            step 1: root has the largest value

            step 2: swap root w/ last element in the array

            step 3: heapify(), excluding last node

            step 4: after heapify(), the second largest element is at the root

            step 5: repeat

            ex) max heap sort

                            80

                        75       60

                    68    55          40  52

                67
                            67

                        75       60

                    68    55          40  52

                80

                must heapify() index 0 - index 6

                            75

                        68       60

                    67    55          40  52

                80

                                52

                        68       60

                    67    55          40  75

                80

                repeat: must heapify() index 0 - index 5 until root index is left after heapify()
    */
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

    /**
     * get root with O(1) CONSTANT time complexity
     */
    public int peek() {

        if(this.isEmpty()) throw new IndexOutOfBoundsException(HEAP_EMPTY);

        int root = this.heap[0];
        return root;
    }

    /*
        HEAP insert():

            step 1: always add to end

            step 2: heapify()

                O(logn) LOGARITHMIC time complexity to fix by swap new item up to root

            step 3: compare new item against parent

            step 4: if greater than parent, then swap

            step 5: repeat

                * ex: add 20 as child to 15 parent

                                22

                            19       18

                    15     3             14     4

                12

                * since 20 is greater than 15 parent, swap

                                22

                            19       18

                    20     3             14     4

                12   15

                * since 20 is greater than 19 parent, swap, afterwards the complete tree has been heapify()

                                22

                            20       18

                    19     3             14     4

                12   15
    */
    public void insert(int value) {

        if(this.isFull()) throw new IndexOutOfBoundsException(HEAP_FULL);

        this.heap[this.size] = value;

        // pass index where we have placed the newValue
        fixHeapAbove(this.size);
        this.size++;
    }

    /*
        HEAP delete():

            step 1: find replacementValue

            step 2: always take rightmost value to keep tree complete

            step 3: heapify()

                O(logn) logarithmic time complexity to fix by swap replacement item up to root

                only need to 3A or 3B, but not both

                    3a heapify()/fixHeapBelow: if replacementValue lesser than parent, then fixHeapBelow, swap replacementValue w/ larger of two children

                    3b heapify()/fixHeapAbove: if replacementValue greater than parent, then fixHeapAbove, swap replacementValue with parent

            step 4: repeat until replacementValue in correct index

                ex) delete 75; replacementValue 67

                                80

                           75       60

                    68    55          40  52

                67

                deleted 75

                            80

                       67       60

                68    55          40  52

                heapify() = fixHeapBelow

                            80

                       68       60

                67    55          40  52

                ex) delete 40; replacementValue 67

                                80

                           75       60

                    68    55          40  52

                67

                deleted 40

                            80

                       75       60

                68    55          67  52

                heapify() = fixHeapAbove

                            80

                       75       67

                68    55          60  52
    */
    public int delete(int index) {

        if(this.isEmpty()) throw new IndexOutOfBoundsException(HEAP_EMPTY);

        // find replacementValue
        int parentIndex = getParent(index);
        int deleteValue = this.heap[index];

        // always take rightmost value to keep tree complete
        this.heap[index] = this.heap[this.size - 1];

        // heapify
        boolean isRoot = (index == 0);
        boolean isReplacementLessThanParent =
            (this.heap[index] < this.heap[parentIndex]);

        if(isRoot || isReplacementLessThanParent) {

            fixHeapBelow(index, this.size - 1);

        } else {

            fixHeapAbove(index);

        }

        this.size--;
        return deleteValue;
    }

    /**
     * heapify()/fixHeapBelow: if replacementValue lesser than parent, then swap replacementValue w/ larger of two children
     *
     * @param index the index of the deleted element
     * @param lastHeapIndex last position of the heap in the array
    */
    private void fixHeapBelow(int index, int lastHeapIndex) {

        int childToSwap;

        while(index >= lastHeapIndex) {

            int leftChild = getChild(index, true);
            int rightChild = getChild(index, false);

            boolean hasLeftChild =
                    (leftChild <= lastHeapIndex);
            boolean hasRightChild =
                    (rightChild < lastHeapIndex);

            // HEAPS: must be a complete tree (NOT ALLOWED: no left child but has a right child)
            if(hasLeftChild) {

                if(!hasRightChild) {

                    childToSwap = leftChild;

                } else {

                    int greatestChildValue = (this.heap[leftChild] > this.heap[rightChild]) ? leftChild : rightChild;

                    childToSwap = greatestChildValue;
                }

                int replacementValue = this.heap[index];
                boolean hasLargerChild = (replacementValue < this.heap[childToSwap]);

                if(hasLargerChild) {

                    // swap replacementValue with the largest child
                    this.heap[index] = this.heap[childToSwap];
                    this.heap[childToSwap] = replacementValue;

                } else {
                    break;
                }
                index = childToSwap;

            } else {
                break;
            }
        }
    }

    /**
     * heapify()/fixHeapAbove: if replacementValue greater than parent, then swap replacementValue with parent
     *
     * @param index child index
    */
    private void fixHeapAbove(int index) {

        int newValue = this.heap[index];

        // HEAPIFY: compare new item against parent, if greater than parent, then shift parent down, repeat
        while((index > 0 && newValue) > (this.heap[getParent(index)])) {
            this.heap[index] = this.heap[getParent(index)];
            index = getParent(index);
        }

        // on discovering correct index for newValue, then insert
        this.heap[index] = newValue;
    }
}
```

# Graphs

<img src="/content/ds_graph.png" alt="data structure graph">

```

```

__Graph Traversal: Breadth-first search vs. Depth-first search__

Use either search algorithm to recursively traverse a graph which is a collection of nodes where each node might point to other nodes that are connected via edges (one-way or two-way)

__depth-first search__

DFS technique starts with a root node and then traverses the adjacent nodes of the root node by going deeper into the graph.

In the DFS technique, the nodes are traversed depth-wise until there are no more children to explore.

Once we reach the leaf node (no more child nodes), the DFS backtracks and starts with other nodes and carries out traversal in a similar manner.

DFS technique uses a stack data structure to store the nodes that are being traversed.

- hasPath(s, t): recursively, nodeS do you have a path to nodeT?
- nodes asks (left-to-right) it's child if it has a path to nodeT, repeat until reached nodeT or null

Detect a cycle in a graph: DFS facilitates to detect a cycle in a graph when we can backtrack to an edge.

Path-finding: As we have already seen in the DFS illustration, given any two vertices we can find the path between these two vertices.

Minimum spanning tree and shortest path: If we run the DFS technique on the non-weighted graph, it gives us the minimum spanning tree and the shorted path.

Topological sorting: Topological sorting is used when we have to schedule the jobs. We have dependencies among various jobs. We can also use topological sorting for resolving dependencies among linkers, instruction schedulers, data serialization, etc.

```
//DFS Technique for undirected graph
public class Graph {

    private int vertices;   // No. of vertices

    // adjacency list declaration
    private LinkedList<Integer> adj_list;

    // graph Constructor: to initialize adjacency lists as per no of vertices
    public Graph(int vertices) {
        this.vertices = vertices;
        this.adj_list = new LinkedList[vertices];

        for (int i = 0; i < vertices; ++i) {
            adj_list[i] = new LinkedList();
        }
    }

    //add an edge to the graph
    public void addEdge(int v, int w) {
        this.adj_list[v].add(w);  // Add w to v's list.
    }

    // helper function for DFS technique
    public void DFS_helper(int v, boolean[] visited) {

        // current node is visited
        visited[v] = true;
        System.out.print(v + " ");

        // process all adjacent vertices
        Iterator<Integer> iterator = this.adj_list[v].listIterator();

        while(iterator.hasNext()) {

            int node = iterator.next();

            if (!visited[node]) {

                // recursion
                DFS_helper(node, visited);
            }
        }
    }

    public void DFS(int v) {

        //initially none of the vertices are visited
        boolean visited[] = new boolean[this.vertices];

        // call recursive DFS_helper function for DFS technique
        DFS_helper(v, visited);
    }
}

public class Main{

    public static void main(String args[]) {

        //create a graph object and add edges to it
        Graph graph = new Graph(5);

        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(0, 3);
        graph.addEdge(1, 2);
        graph.addEdge(2, 4);

        //print the DFS Traversal sequence
        System.out.println(
            "Depth First Traversal for given graph with 0 as starting vertex: "
        );

        graph.DFS(0);
    }
}
```

__breadth-first Search__

This means we traverse the graph level wise. When we explore all the vertices or nodes at one level we proceed to the next level.

- hasPath(s, t): recursively, does nodeS do you have a path to nodeT?

- nodes checks if any of its children are nodeT, if no edges to first level children, then check next level and repeat

Garbage collection: One of the algorithms used by the garbage collection technique to copy Garbage collection is “Cheney’s algorithm”. This algorithm uses a breadth-first traversal technique.

Broadcasting in networks: Broadcasting of packets from one point to another in a network is done using the BFS technique.

GPS navigation: We can use the BFS technique to find adjacent nodes while navigating using GPS.

Social networking websites: BFS technique is also used in social networking websites to find the network of people surrounding a particular person.

Shortest path and minimum spanning tree in un-weighted graph: In the unweighted graph, the BFS technique can be used to find a minimum spanning tree and the shortest

```
//undirected graph represented using adjacency list.
public class Graph {

    private int vertices;   // No. of vertices
    private LinkedList<Integer> adj_list[]; //Adjacency Lists

    // graph Constructor:number of vertices in graph are passed
    public Graph(int vertices) {
        this.vertices = vertices;
        this.adj_list = new LinkedList[v];

        // create adjacency lists
        for (int i=0; i < vertices; ++i) {
            this.adj_list[i] = new LinkedList();
        }
    }

    // add an edge to the graph
    public void addEdge(int v,int w) {
        this.adj_list[v].add(w);
    }

    // BFS traversal from the root_node
    public void BFS(int root_node) {

        // initially all vertices are not visited
        boolean visited[] = new boolean[this.vertices];

        // BFS queue
        LinkedList<Integer> queue = new LinkedList<>();

        // current node = visited, insert into queue
        visited[root_node] = true;

        queue.add(root_node);

        while (queue.size() != 0) {

            // deque an entry from queue and process it
            root_node = queue.poll();
            System.out.print(root_node + " ");

            // get all adjacent nodes of current node and process
            Iterator<Integer> iterator = this.adj_list[root_node].listIterator();

            while (iterator.hasNext()) {

                int node = iterator.next();

                if (!visited[node]) {

                    visited[node] = true;
                    queue.add(node);
                }
            }
        }
    }
}

public class Main{

    public static void main(String args[]) {

        //create a graph with 5 vertices
        Graph graph = new Graph(5);

        //add edges to the graph
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(0, 3);
        graph.addEdge(1, 2);
        graph.addEdge(2, 4);

        //print BFS sequence
        System.out.println("Breadth-first traversal of graph with 0 as starting vertex:");
        graph.BFS(0);
    }
}
```

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

        int start = 0;
        int end = array.length;

        recursivePartition(array, start, end);
        return array;
    }

    // RECURSION: a continuously self-calling algorithm & each call on the call-stack waits for the algorithm to reach a base case/breaking condition for a return value.
    private static void recursivePartition(int[] array, int start, int end) {

        // RECURSIVE BASE CASE: the breaking condition that initiates an upward propagation of return of values for the waiting calls that results in a call-stack resolution or overflow
        int partitionLength = end - start;
        boolean isBaseCase = (partitionLength < 2);

        if(isBaseCase) return;

        int midpoint = (start + end) / 2;

        // RECURSION + DIVIDE & CONQUER: partition LEFT side FIRST w/ midpoint via start & end indices
        // [20, 35, -15] ->
        //      [20] [35, -15] ->
        //          [20] [35] [-15]

        recursivePartition(array, start, midpoint);

        // RECURSION + DIVIDE & CONQUER: then RIGHT side with midpoint via start & end indices
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

            tempArray[tempIndex++] = (currentLeftElement <= currentRightElement) ? array[i++] : array[j++];
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

__QUICK SORT (DFS):__

Big(O) LOGARITHMIC TIME COMPLEXITY = O(logn) = O of log to the base 2 n

- repeatedly dividing array in half during splitting

SPACE COMPLEXITY: in-place algorithm that doesn't use extra memory

UNSTABLE ALGORITHM:

- if there are duplicate elements, no guarantee that their original order will be preserved,

- since quick sort is predicated on moving elements around a pivotIndex for recursive partitions

QUICK SORT LOGIC:

divide & conquer algorithm:

- splitting base problem into several mini-problems, solving mini-problems, and then merging mini-solutions to solve base problem

recursive algorithm:

- calls itself until reaching a base case and then feeds return values to itself to solve backwards

PHASE 1: partitioning step/pivotIndex splitting

1. divide the array into two sub-arrays (left & right partitions)

- identify pivot index for logical splitting (in-place = no new arrays)
- each element and it's respective index eventually serves as the pivot index
- CHECK: pivot index serves as boundary for 2 sibling sub-arrays that prevent crossover

2. then recursively divide each subsequent array into two arrays

3. UNTIL you have multiple sorted arrays of 1 length (each containing the pivotIndex element at it's correct position)

- in left sub-array, elements less than pivotIndex element are moved to the left during traversal
- in right sub-array, elements greater than pivotIndex element are moved to the right during traversal

- AS A RESULT, element at pivotIndex will be in the middle AND in its correct position

```
right-to-left first
left-to-right second
                                             [20, 35, -15, 7, 55, 1, -22]

                            [-15, 7, 20, 35]       pivotIndex = 7            [-22, 1, 7, 55]

            [-15, 7]    pivotIndex = 7  [7, 20, 35]            [-22, 1]    pivotIndex = 1      [1, 7, 55]

    [-15] && [7]     [7, 20] pivotIndex = 20 [20, 35]       [-22] && [1]        [1, 7] pivotIndex = 7 [7, 55]

                    [7] && [20] && [35]                                     [1] && [7] && [55]
```

PHASE 2: merging

- MERGING = sorting elements/pivotIndex in respective 1-element array that are starting from bottom-to-up in-place

- handle left side first, then right side

- merge all sibling arrays on left & right side before proceeding to higher level to recursively merge resulting sibling arrays

- after correct index for pivotIndex element has been FOUND after each traversal, re-assign pivotIndex for subsequent sub-arrays/partitions

```
@Test
void quickSort_success() {

    int[] input = {8,4,3,6,1,7,2,9,5};
    int start = 0;
    int end = input.length;

    int[] expected = {1,2,3,4,5,6,7,8,9};
    int[] actual = quickSort(input, start , end);

    assertEquals(
        Arrays.toString(expected),
        Arrays.toString(actual)
    );
}

@Test
void quickSort_fail_badInput() {

    int[] input = {};
    int start = 0;
    int end = input.length;

    int[] actual = quickSort(end, start , end);

    assertNull(actual);
}

public static int[] quickSort(int[] array, int start, int end) {

    if(array.length == 0) return null;

    boolean isBaseCase = ((end - start) < 2);

    if(isBaseCase) return array;

    // use pivotIndex to move smaller elements left & larger elements right for recursive partitions of 2+ length
    int pivotIndex = getPivot(array,start, end);

    // use recursion to subsequently shift elements left or right in relation to pivot index
    // left partition
    array = quickSort(array, start, end);

    // right partition
    array = quickSort(array, (pivotIndex + 1), end);

    return array;
}

private static int getPivot(int[] array, int start, int end) {

    // use first element in the inputArray || sub-array as the pivot
    int pivotIndex = nums[start];

    // QUICK SORT in-place: alternate between traversing right-to-left & left-to-right & shift relative to pivot
    // traverse left-to-right
    int i = start;

    // traverse right-to-left
    int j = end;

    // define partitions by ensuring no crossover between traversing index
    while(i < j) {

        // LEFT PARTITIONS: decrement j to traverse array right-to-left for an element less than the pivot
        while(i < j && (nums[--j] >= pivotIndex));

        // stop traversal when i and j cross each other to maintain partitions
        boolean inPartitionBound = (i < j);

        // use recursion to subsequently shift elements left or right in relation to pivot index
        if(inPartitionBound) {

            // FOUND 1st element less than pivot during traversal of respective partition: so move element at index j to index i (move to LEFT of pivotIndex)
            nums[i] = nums[j];
        }

        // RIGHT PARTITIONS: decrement i before execution to traverse array left-to-right for an element greater than the pivot
        while(i < j && (nums[++i] <= pivotIndex));

        if(inPartitionBound) {

            // FOUND 1st element greater than pivot during traversal of respective partition: so move element at index i to index j (move to RIGHT of pivotIndex)
            nums[j] = nums[i];
        }
    }

    // index j will become the new pivot index for subsequent sub-arrays/partitions
    nums[j] = pivotIndex;

    return j;
}
```


__REGEX character class__

- character classes allow us to specify characters to filter in a pattern

```
    \ = escape special meaning of a character

    . = matches everything

    \. = string value of a period

    \d = digit 0-9

    \w = letter, digit, or underscore

    \s = whitespace character

    \D = not a digit

    \W = not a word character

    \S = not a whitespace character
```

__REGEX boundary matcher__

- character classes allow us to specify characters in a GROUP/RANGE to filter in a pattern

```
    [] = character classes allow us to specify groups/ranges of characters

    [^] = anything that is NOT the specified characters in the brackets with the carrot symbol

        [^k] = anything but the lowercase letter k

    ^ = carrot anchor species the search string has to start with defined regular expression

        ^\d{3}

    '$' = dollar sign boundary denotes the end of string or line

    \b = word boundary

        ex: \b\w+\b = select only and every word

            'hello world I am typing'

    | = the pipe character in regex denotes logical or

        "Mr|Mrs|Ms"

    () = parenthesis represent whole group

        (\(\d{3}\)|\d{3}) \d{3} \d{4}
```

__REGEX quantifiers__

- specify how many times a specific character should occur in a pattern

```
    + = one or more

    {x} = exactly x times.

        {3} = 3 times

    {3,5} = 3 to 5 times

    {4,} = four or more times

    * = zero or more times

    ? = once or none (optional)
```

# Test Driven Development (TDD)

writing code that tests your other code to ensure a level of performance quality when your app is in production; making refactoring and collaboration safer and bug-free

1. development BEGINS by writing RED failing tests

2. once tests are written, write the MINIMUM amount of GREEN code necessary to make tests pass

3. refactor = clean up the code, while ensuring that tests still pass

4. once tests pass, a feature is considered complete

__TDD JUNIT__

1. update project structure JUnit library dependency to compile

```
   File -> project structure -> Modules -> Dependencies Tab ->
       Export window -> Junit ->
           open dropdown -> change "Test" to "Compile" -> Ok
```

2. add JUnit Library

- right-click add "JUnit" to class path

- select "Use JUnit from IntelliJ IDEA distribution"

- click Ok

3. define class, method signatures, & test suite

4. create JUnit Test class & generate methods to test in root

- click yellow light bulb onHover over independent class name

- FIX if IDE is unable to identify built-in JUnit Test class

- select specific methods to test

5. BEFORE running, add fail(NOT_IMPLEMENTED) to each Test class method stub

6. run expected failing tests suite

7. review run configuration for all tests
  want to test class in application, NOT the application itself

- right-click outside created Test class & select run Test class
- right-click outside created Test class & select modify run configuration
- review configurations & click Ok
- review right-corner dropdown is respective Test suite

8. setup tests objects run before & after teardown every test run

```
public class AnimalTest {

    private static final String BEFORE_ALL = "STATIC execute only once before all test suit is run, read data fro mdb for tests";
    private static final String BEFORE_EACH = "execute code in setup() before each test is run";
    private static final String AFTER_EACH = "execute code in setup() after each test is run";
    private static final String AFTER_ALL = "STATIC execute only once after all test suit is run";

    private Animal animal;

    @BeforeAll
    static void beforeAll() {
        System.out.println(BEFORE_ALL);
    }

    @BeforeEach
    void beforeEach() {
        System.out.println(BEFORE_EACH);
        animal = new Animal("Teddy", "Bear");
    }

    @AfterEach
    void afterEach() {
        System.out.println(AFTER_EACH);
    }

    @AfterAll
    static void afterAll() {
        System.out.println(AFTER_ALL);
    }

    @Test
    void hasEaten_true() {

        int testHunger = 80;

        boolean actual = animal.hasEaten(testHunger);
        assertTrue(actual);
    }

    @Test
    void hasEaten_false() {

        int testHunger = 80;

        boolean actual = animal.hasEaten(testHunger);
        assertFalse(actual);
    }
}
```

9. write test method assertions that test against class functionality

- in testSuite, click on green arrow/red x in gutter next to specific method to test

- review only passing or only failing tests with toggle in top-left of Test window

```
// JUnit TRY-CATCH: handle expected exceptions handing modify @Test annotation

try {
    double balance = checkingsAccount.withdraw(600.00, false);
    assertEquals(400.00, balance, 0);
} catch(IllegalArgumentException e) {
    System.out.println(e.getMessage());
}
```

BEST PRACTICE:

write easily understood test method names

```
getBalance_deposit()
getBalance_withdraw()
```

write on 1 independent assertion for 1 independent test

setup any independent class instances that can be reused (without cross-pollination) on each test method

```
assertEquals(expectedValue, actualTestValue);

assertNotEquals(expectedValue, actualTestValue);

assertTrue(actualTestValue, failMsg);

assertFalse(actualTestValue, failMsg);

// consider two arrays equal if length & every element in order identical
assertArrayEquals(expectedArray, actualTestArray);

assertNull(actualTestValue);

// easy-to-read check for null values
assertNotNull(actualTestValue);

assertSame(expectedValue, actualTestValue);

// compares object references, unlike assertEquals that checks if instances are the same
assertNotSame(expectedValue, actualTestValue);

// compare the actual value against a matcher range of values
assertThat(expectedValue, actualTestValue);
```

10. write method implementation in file

11. individually run implemented functions until all failing tests resolved in test suite

# Content Management System

A content management system (CMS) is a tool that allows you to build all of the pieces of your website - from text to photos to widgets - via an easy-to-use interface.

With a CMS like Wordpress, Wix, or Atlassian's Bitbucket, you don’t need to write your own code; instead, you can apply pre-created templates and plug-ins to quickly and efficiently build a website.

# Project Management

Enterprise project management software helps businesses accurately measure and control scope creep (costs, time, and resources) and consistently deliver projects that are in alignment with business goals to ensure project success.

__Agile Methodology__

Agile project management takes an iterative approach to development by creating several incremental steps with regular feedback intervals (sprints).

The development team can only accept work that it has the CAPACITY for. The product owner doesn't push work to the team or commit them to arbitrary deadlines. The development team pulls work from the program's backlog as it can accept new work.

AGILE UPSIDE

- A project requirement is segmented into smaller pieces, which are then prioritized by importance.

- Promotes collaboration, especially with the customer.

- Adjusts at regular intervals to ensure a customer’s needs are met

AGILE DOWNSIDE

- Critical path and inter-project dependencies may not be clearly defined as in waterfall

Agile Scrum uses two-week sprints to get work done. These sprints are planned in advance, executed, and then reviewed at the end of the two-week period. During sprint planning, the team creates a sprint backlog. The team completes these backlog tasks during the sprint, managing the work among themselves.

To build an AGILE roadmap, product owners take into account market trajectories, value propositions, and engineering constraints.

<img src="/content/jira-agile.png" alt="agile project management">

__Jira + Agile__

Jira software is the project management tool for AGILE teams, customizable for any type of project.

- Teams can start with a project template or create their own custom workflow.

- Jira issues, also known as tasks, tracks each piece of work that passes through the workflow steps to completion.

- Jira's automation engine enables teams to easily automate tasks and processes.

- With all project information in one place, reports can also be generated to track progress, productivity and ensure nothing slips.

__Waterfall Methodology__

The waterfall project management approach follows a linear, sequential formula.

The waterfall project management approach entails a clearly defined sequence of execution with project phases that do not advance until a phase receives final approval.

- Once a phase is completed, it can be difficult and costly to revisit a previous stage.

WATERFALL UPSIDE

- Requires less coordination due to clearly defined phases that are sequential processes

WATERFALL DOWNSIDE

- It's harder to break up and share work because of stricter phase sequences

- thus teams are more specialized & the risk of time waste due to delays and setbacks are higher during phase transitions

__Trello + Waterfall__

Trello Kanban’s board visualizes the team’s workflow.

- The board is split into categories of work to be done, work in progress, and completed work, and teams can add more categories as necessary to better visualize their process.

The Trello tasks are placed on cards and team members who are assigned to that task are added to the card.

- The card moves through the workflow as progress is made on completing the task.

<img src="/content/trello-waterfall.png" alt="agile project management">

Trello project management workflow Phases:

- Backlog
- In Progress
- Blocked/Paused
- Ready for Launch
- Live

# SQL

SQL is a query language, whereas MySQL is a relational database that uses SQL to query a database

__RELATIONAL DATABASES__

an interconnected database that holds data tables, a collection of columns (headers) and rows (data)

- all the data is structured into a uniform manner through data table constraints

- you can have multiple tables joined together by a defined relationship

- relationships help force constraints using primary keys and foreign keys to give meaning

- a relational database's storage is concentrated: 1 node contains an entire copy of the data, not partitioned by default

- relational databases can be scale in 2 manners:

  - vertical scaling: build a better machine via more memory, faster hard disk, better cpu

  - horizontal scaling: simply add more machines (servers)

- relational databases can be accessed through raw SQL

__NON-RELATIONAL DATABASES__

collected tables, documents, or graphs hold data together but CANNOT be joined together by a relationship, but rather organized by key-value stores, that is distributed over multiple servers to be built to scale with high performance & low latency

- its best to use non-relational databases when the data model fits (graphs)

- non-relational database storage relies on hashing functions for the input and the result is used to identify the partition where the data is stored

- non-relational database scale is easily improved by adding more partitions that function improved & improved independently

- when accessing a non-relational database: many are no-sql databases that have their own CRUD (create, read, update, delete) functionality that rely on key-value stores

  - non-relational databases rely on REST APIs to hit a specific endpoint that comes with certain functionality

__SQL RELATIONSHIPS__

when using relational databases, always compartmentalize the dataset into separate tables

- this improves performance because you are only getting the data that you need

if you need data originating from different tables, then you can build queries that join said necessary tables by shared relationship

SQL JOIN Relationships = the different ways two or multiple data tables are related -- there are 3 main types of JOIN RELATIONSHIPS

    1. one-to-one relationships (not very common)

        ex: 1 customer-to-1 customer details relationship

    2. one-to-many relationships (most common)

        ex: 1 book-to-many book reviews relationship

    3. many-to-many relationships (relatively common)

        ex: many authors-to-many books relationship (a book can have multiple authors)

__PRIMARY KEY AUTO_INCREMENT__

when creating a table, a primary key ensures one column that is always unique for joined relationships between 2 or more tables

```
CREATE TABLE students(
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(20)
);

SHOW TABLES;
DESC students;
```

__FOREIGN KEY__

when creating a table, a foreign key references to a shared attribute in another table 
this constraint explicitly guards against bad data input

```
CREATE TABLE series(
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(20)
);

CREATE TABLE reviewers(
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(20)
);

CREATE TABLE REVIEWS(
    id INT AUTO_INCREMENT PRIMARY KEY,
    series_id INT,
    reviewers_id INT,
    FOREIGN KEY(series_id)
        REFERENCES series(id)
        ON DELETE CASCADE,
    FOREIGN KEY(reviewers_id)
        REFERENCES reviewers(id)
        ON DELETE CASCADE
);
```

__JOIN__

when you SELECT data from multiple tables and join them, you are temporarily consolidate them in a meaningful way

an INNER JOIN only shows data that overlaps between multiple data tables (it can be visualized as the middle of a venn diagram with no nulls)

a LEFT or RIGHT join will ALSO show data overlap IN ADDITION TO the null data pairs (the specified left or right section + the middle of a venn diagram)

It is common for LEFT OR RIGH joins to have nulls, anything that does not fall in the overlap section of a venn diagram is a null data pair

<img src="/content/SQL_joins.jpeg" alt="SQL Joins Diagram">

# Serialization

Serialization is the process of converting a data object into a series of bytes that saves the state of the object in an easily transmittable form - like a file, database, memory.

- a data object is a combination of code and data represented within a region of data storage

Deserialization is the reverse process where it reads a stream of bytes from a data source - like a file, database, or memory - and converts it back into the original data object - in Java, the deserialized data needs to be cast back to the original dataType object.

<img src="/content/serialization.png">

```
/**
 * ObjectOutputStream() takes a serializable object and converts it into a sequence/stream of bytes.
 */
public static void serialize(Book book, String filename) throws Exception {

    FileOutputStream file = new FileOutputStream(fileName);
    ObjectOutputStream out = new ObjectOutputStream(file);

    // serialize the book data object
    out.writeObject(book);

    // ensure that the serialization/deserialization resources are no longer unnecessarily utilizing memory or processing after task completion
    out.close();
    file.close();
}

/**
 * ObjectInputStream() reads a stream of bytes and converts it back into a data object.
 * That data object must then be cast back into the the original dataType object.
 */
public static Book deserialize(String fileName) throws Exception {

    FileInputStream file = new FileInputStream(fileName);
    ObjectInputStream in = new ObjectInputStream(file);

    // deserialization of a byte stream
    Book book = (Book) in.readObject();

    // ensure that the serialization/deserialization resources are no longer unnecessarily utilizing memory or processing after task completion
    in.close();
    file.close();

    // return the deserialized original data object
    return book;
}
```

__TRANSIENT__

use the transient keyword to ignore class fields during serialization that do not represent the state of the object or for any non-serializable references

The serialization process is dependent on implementing instances: classes that are eligible for serialization need to implement the Serializable interface in Java.

```
public class Book implements Serializable {

    // OOP ENCAPSULATION private class fields
    private static final long serialVersionUID = -2936687026040726549L;
    private String bookName;

    private transient String description;
    private transient int copies;

    // in the given example, an OOP constructor isn't required since all class fields will be set to null or 0 (depending on their dataType) on instantiation

    // OOP GETTERS & SETTERS 
}
```

```
public class BookTest {

    // CONSTANTS/static class variables assigned FINAL value before compilation/instantiation
    private static final String JAVA_REF = "Java Reference"; 

    @Test
    void bookSerialization() {

        Book book = new Book();

        book.setBookName(JAVA_REF);
        book.setDescription("description will not be saved due to transient keyword in class field definition");
        book.setCopies(25);

        // the below test results with the bookName having been properly persisted.

        String expected = JAVA_REF; 
        String actual = book.getBookName();
        assertEquals(expected, actual);

        // due to the transient keyword, the below tests results with the copies field having a value of 0 and the description is null instead of the original values.

        int expectedCopies = 0;
        int actualCopies = book.getCopies();
        assertEquals(expectedCopies, actualCopies);

        assertNull(book.getDescription());
    }
}
```

# Concurrency

Software that can execute processes simultaneously (one task doesn't have to complete before another one can start)

<img src="/content/concurrency.jpeg">

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

__THREADS .start()__

only JVM executes .run() for a given single Thread (always a new Thread instance), including priority-assigned threads, and CANNOT assume Thread instance execution order

```
new Thread() {
    @Override
    public void run() {
        System.out.println("Hello from anonymous class Thread")
    }
}.start();
```

__MULTI-THREADING__

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

# Synchronization

the process of semi-controlling/influencing when threads execute code and therefore when they can access the heap is called synchronization.

- when working with threads, we have to synchronize all areas where we think or where interference can happen.

__THREAD SYNCHRONIZATION code blocks__

<img src="/content/thread_synchronization.png">

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

<img src="/content/thread_synchronization_locks.png">

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

# MapReduce

MapReduce is a programming model or pattern within the Hadoop framework that is used to access big data stored in the Hadoop File System (HDFS).

- MapReduce facilitates concurrent processing by splitting petabytes of data into smaller chunks, and processing them in parallel on Hadoop commodity servers.

With MapReduce, rather than sending data to where the application or logic resides, the logic is executed on the server where the data already resides, to expedite processing.

- Data access and storage is disk-based—the input is usually stored as files containing structured, semi-structured, or unstructured data, and the output is also stored in files.

At the crux of MapReduce are two functions: Map and Reduce. They are sequenced one after the other.

- The Map function takes input from the disk as <key,value> pairs, processes them, and produces another set of intermediate <key,value> pairs as output.

- The Reduce function also takes inputs as <key,value> pairs, and produces <key,value> pairs as output.

<img src="/content/map_reduce.png" alt="map reduce">

The types of keys and values differ based on the use case.

- All inputs and outputs are stored in the HDFS.
- While the map is a mandatory step to filter and sort the initial data, the reduce function is optional.

```
<k1, v1> -> Map() -> list(<k2, v2>)
<k2, list(v2)> -> Reduce() -> list(<k3, v3>)
```

Mappers and Reducers are the Hadoop servers that run the Map and Reduce functions respectively. It doesn’t matter if these are the same or different servers.

__STEP 1: create MAPS__

The input data is first split into smaller blocks. Each block is then assigned to a mapper for processing.

For example, if a file has 100 records to be processed, 100 mappers can run together to process one record each. Or maybe 50 mappers can run together to process two records each. The Hadoop framework decides how many mappers to use, based on the size of the data to be processed and the memory block available on each mapper server.

__STEP 2: shuffle map to REDUCERS__

After all the mappers complete processing, the framework shuffles and sorts the results before passing them on to the reducers. A reducer cannot start while a mapper is still in progress. All the map output values that have the same key are assigned to a single reducer, which then aggregates the values for that key.

__Combine and Partition__

There are two intermediate steps between Map and Reduce.

Combine is an optional process. The combiner is a reducer that runs individually on each mapper server. It reduces the data on each mapper further to a simplified form before passing it downstream.

This makes shuffling and sorting easier as there is less data to work with. Often, the combiner class is set to the reducer class itself, due to the cumulative and associative functions in the reduce function. However, if needed, the combiner can be a separate class as well.

Partition is the process that translates the <key, value> pairs resulting from mappers to another set of <key, value> pairs to feed into the reducer. It decides how the data has to be presented to the reducer and also assigns it to a particular reducer.

The default partitioner determines the hash value for the key, resulting from the mapper, and assigns a partition based on this hash value. There are as many partitions as there are reducers. So, once the partitioning is complete, the data from each partition is sent to a specific reducer.

__MapReduce Example__

Consider an ecommerce system that receives a million requests every day to process payments.

- There may be several exceptions thrown during these requests such as "payment declined by a payment gateway," "out of inventory," and "invalid address."

- A developer wants to analyze last four days' logs to understand which exception is thrown how many times.

The objective is to isolate use cases that are most prone to errors, and to take appropriate action. For example, if the same payment gateway is frequently throwing an exception, is it because of an unreliable service or a badly written interface? If the "out of inventory" exception is thrown often, does it mean the inventory calculation service has to be improved, or does the inventory stocks need to be increased for certain products?

The developer can ask relevant questions and determine the right course of action.

- To perform this analysis on logs that are bulky, with millions of records, MapReduce is an apt programming model.

- Multiple mappers can process these logs simultaneously: one mapper could process a day's log or a subset of it based on the log size and the memory block available for processing in the mapper server.

```
/*
    The parameters—MapReduce class name, Map, Reduce and Combiner classes, input and output types, input and output file paths—are all defined in the main function.
    The Mapper class extends MapReduceBase and implements the Mapper interface.
    The Reducer class extends MapReduceBase and implements the Reducer interface.
 */
public static void main(String[] args) throws Exception {

    JobConf conf = new JobConf(ExceptionCount.class);
    conf.setJobName("exceptioncount");

    conf.setOutputKeyClass(Text.class);
    conf.setOutputValueClass(IntWritable.class);

    conf.setMapperClass(Map.class);
    conf.setReducerClass(Reduce.class);
    conf.setCombinerClass(Reduce.class);

    conf.setInputFormat(TextInputFormat.class);
    conf.setOutputFormat(TextOutputFormat.class);

    FileInputFormat.setInputPaths(conf, new Path(args[0]));
    FileOutputFormat.setOutputPath(conf, new Path(args[1]));

    JobClient.runJob(conf);
}
```

Step 1: CREATE MAPS

For simplification, let's assume that the Hadoop framework runs just four mappers: Mapper 1, Mapper 2, Mapper 3, and Mapper 4.

The value input to the mapper is one record of the log file. The key could be a text string such as "file name + line number." The mapper, then, processes each record of the log file to produce key value pairs. Here, we will just use a filler for the value as '1.' The output from the mappers look like this:

```
Mapper 1 -> <Exception A, 1>, <Exception B, 1>, <Exception A, 1>, <Exception C, 1>, <Exception A, 1>
Mapper 2 -> <Exception B, 1>, <Exception B, 1>, <Exception A, 1>, <Exception A, 1>
Mapper 3 -> <Exception A, 1>, <Exception C, 1>, <Exception A, 1>, <Exception B, 1>, <Exception A, 1>
Mapper 4 -> <Exception B, 1>, <Exception C, 1>, <Exception C, 1>, <Exception A, 1>
```

Assuming that there is a combiner running on each mapper—Combiner 1 … Combiner 4—that calculates the count of each exception (which is the same function as the reducer), the input to Combiner 1 will be:

```
<Exception A, 1>, <Exception B, 1>, <Exception A, 1>, <Exception C, 1>, <Exception A, 1>
```

Step 2: COMBINE

The output of Combiner 1 will be:

```
<Exception A, 3>, <Exception B, 1>, <Exception C, 1>
```

The output from the other combiners will be:

```
Combiner 2: <Exception A, 2> <Exception B, 2>
Combiner 3: <Exception A, 3> <Exception B, 1> <Exception C, 1>
Combiner 4: <Exception A, 1> <Exception B, 1> <Exception C, 2>
```

Step 3: PARTITION

After this, the partitioner allocates the data from the combiners to the reducers. The data is also sorted for the reducer.

The input to the reducers will be as below:

```
Reducer 1: <Exception A> {3,2,3,1}
Reducer 2: <Exception B> {1,2,1,1}
Reducer 3: <Exception C> {1,1,2}
```

If there were no combiners involved, the input to the reducers will be as below:

```
Reducer 1: <Exception A> {1,1,1,1,1,1,1,1,1}
Reducer 2: <Exception B> {1,1,1,1,1}
Reducer 3: <Exception C> {1,1,1,1}
```

Here, the example is a simple one, but when there are terabytes of data involved, the combiner process’ improvement to the bandwidth is significant.

Step 4: REDUCE

Now, each reducer just calculates the total count of the exceptions as:

```
Reducer 1: <Exception A, 9>
Reducer 2: <Exception B, 5>
Reducer 3: <Exception C, 4>
```

The data shows that Exception A is thrown more often than others and requires more attention. When there are more than a few weeks' or months' of data to be processed together, the potential of the MapReduce program can be truly exploited.

# Distributed Cache

__CACHE__

computer short-term memory & caching means saving frequently accessed data in-memory

Accessing cache is typically faster than accessing the origin data source again

- You know Accessing data from RAM is always faster than accessing it from the hard drive

__DISTRIBUTED CACHE__

A cache which has its data spread across several nodes in a (a) cluster, (b) across several clusters or (c) across several data centres located around the world

👉 A Distributed cache under the covers is a Distributed Hash Table which has a responsibility of mapping Object Values to Keys spread across multiple nodes.

👉 A hash table manages the addition, deletion, failure of nodes continually as long as the cache service is online. Distributed hash tables were originally used in the peer to peer systems.

👉 routinely check data integrity bia cache invalidation

👉 caches evict data based on the LRU (Least Recently Used policy) uses a Doubly-Linked-List to manage the data pointers, which is the most important part of the data-structure.

__CACHE INVALIDATION__

If any data is modified in the database, it should be invalidated or modified in the cache also; if it is not so, this can cause inconsistent application behavior.

Read-Through

<img src="/content/distributed-cache-read-through.png">

- The data is written into the cache and the corresponding database at the same time.

- This scheme maintains the complete data consistency between the cache and the main storage. Even this scheme also ensures that nothing will get lost in case of a crash, power failure, or any other system disruptions.

- The disadvantage of this scheme is the Higher Latency, since every write operation is done twice before returning success to the client😔

Write-Through

<img src="/content/distributed-cache-write-through.png">

- In this strategy, every information directly written to the database just bypassing the cache.

- The disadvantage of this scheme is the Higher Latency if in case of a read request for recently written data will create a “cache miss”😯 and then the read request must be made on back-end storage.

Write-Back

<img src="/content/distributed-cache-write-back.png">

- The data is written to cache only and completion is immediately confirmed to the client. The write to the permanent storage is done after specified intervals or under certain conditions. This results in low latency and high throughput for write-intensive applications.

- However, this speed comes with the risk of data loss in case of a crash or other adverse event because the only copy of the written data is in the cache.

__DISTRIBUTED CACHE BENEFITS__

Businesses (like health services, military, stock markets) cannot afford to have their services go offline.

👉 Memcache is most popular cache which is used by Google Cloud Google Cloud🌨  in its Platform As A Service.

👉 Redis NoSQL data store is an open-source in-memory distributed system which supports other data structures too such as distributed lists, queues, strings, sets, sorted sets.

1. Scalability

👉 the capacity of a system to handle a growing amount of work by adding resources to the system

2. High Availability

👉 if availability tends to 100% its called high availability. To do this, it contains backup components to which it automatically switches (fails over) when an active component stops working.

3. Fault-tolerance

the ability of a system (computer, network, cloud cluster, etc.) to continue operating without interruption when one or more of its components fail.

👉 an OS’s ability to recover and tolerate faults without failing can be handled by hardware, software, or a combined solution leveraging load balancers.

👉 fault-tolerant systems use backup components that automatically take the place of failed components, ensuring no loss of service.

__USE CASES__

1. Database Caching

The Cache can be placed between Application Server and Database. Where access the data from cache instead of main datastore which frequently accesses data in-memory to cut down latency & unnecessary load on it. There is no DB bottleneck when the cache is implemented.

2. User Sessions Storing

User sessions are mostly stored in the cache to avoid losing the user information in case any of the instances go down.
If any of the instance goes down, a new instance spins up, reads the user data from the cache & continues the session without having the user notice anything amiss.

3. In-memory Data Lookup

If you have a mobile / web app front end you might want to cache some information like user profile, some historical data, or some API response according to your use cases. Caching will help in storing such data.

__CACHE EVICTION__

A cache eviction algorithm is a way of deciding which element to evict when the cache is full.

- First In First Out (FIFO): The cache evicts the first block accessed first without any regard to how often or how many times it was accessed before.

- Last In First Out (LIFO): The cache evicts the block accessed most recently first without any regard to how often or how many times it was accessed before.

- Least Recently Used (LRU): Discards the least recently used items first. Best 🙂

- Most Recently Used (MRU): Discards, in contrast to LRU, the most recently used items first.

- Least Frequently Used (LFU): Counts how often an item is needed. Those that are used least often are discarded first.

<img src="/content/distributed-cache.png">

# Internet Fundamentals

__COMPUTER NETWORK__

a set of independent computer systems connected by telecommunications links for the purpose of sharing information & resources.

<img src="/content/computer-network.png">

__INTERNET__

an independent global system of computer networks connected by a collection of protocols implemented in software and hardware designed to interconnect all types of networks like cell phones, Ethernet, wifi, etc.

<img src="/content/internet.jpeg">

__PROTOCOLS__

an agreements on a technical standard that is implemented by software or hardware devices.

__MODEM__

a hardware device that transforms between physical states (analog) and bits (digital) for the internet

<img src="/content/modem.png">

__IP ADDRESS__

An Internet Protocol (IP) address identifies geographic location based on the organization that “owns” it.

Groups of addresses are allotted to various organizations by Internet Assigned Numbers Authority (IANA)

Each computer on the Internet is assigned an IP Address
consisting of four numbers between 0 and 255 inclusive:

```
128.2.13.163
```

__ROUTING__

There are multiple paths from one node
(computer) to another

<img src="/content/routing.png">

Two network nodes (e.g. phones) establish a dedicated connection via one or more switching stations.

__PACKET SWITCHING__

We attach the source and destination IP addresses to the message & two network nodes (e.g. computers) communicate by breaking the message up into small packets

Routers forward packets toward the destination

the table stored in a router tells it which neighbor to send the packet to, based on IP address of destination

__INTERNET STRUCTURE__

the Core provides transport services to edges

- the routers forward packets

- Internet Service Providers (ISPs) provide data transmission media (fiber optic etc.)

- domain name servers (DNS) provide directory of host
names (more on this next time)

the Edges provide the services people use

- individual users, “hosts”

- private networks (corporate, educational, government…)

- business, government, nonprofit services

<img src="/content/packet-switching.png">

__END-TO-END PRINCIPLE__

Routers should only be responsible for getting data quickly from its source to its destination.

- Equality of uses: routers can’t discriminate based on type of communication (net neutrality

Everything else is responsibility of edges

- error detection & recovery

- confidentiality via encryption

Issues:

- lack of trust because of bad actors on the Internet

- profit opportunities for ISPs

- corporate and government monitoring of communications

__NET NEUTRALITY__

All communications are treated equally regardless of source, destination, or type

But some governments already censor or otherwise
control the Internet within their borders

# Service-Oriented Architectures (SOA)

<img src="/content/soa.png">

A method of software development that uses easily switchable software components called services to create business applications.

1. Interoperability

Each service in SOA includes description documents that specify the functionality of the service and the related terms and conditions. Any client system can run a service, regardless of the underlying platform or programming language.

- For instance, business processes can use services written in both C# and Python. Since there are no direct interactions, changes in one service do not affect other components using the service.

2. Loose coupling

Services in SOA should be loosely coupled, having as little dependency as possible on external resources such as data models or information systems. They should also be stateless without retaining any information from past sessions or transactions. This way, if you modify a service, it won’t significantly impact the client applications and other services using the service.

3. Abstraction

Clients or service users in SOA need not know the service's code logic or implementation details. To them, services should appear like a black box. Clients get the required information about what the service does and how to use it through service contracts and other service description documents.

4. Granularity

Services in SOA should have an appropriate size and scope, ideally packing one discrete business function per service. Developers can then use multiple services to create a composite service for performing complex operations.

__SERVICES__

In service-oriented architecture (SOA), services function independently and provide functionality or data exchanges to their consumers. The consumer requests information and sends input data to the service. The service processes the data, performs the task, and sends back a response.

- For example, if an application uses an authorization service, it gives the service the username and password. The service verifies the username and password and returns an appropriate response.

__COMMUNICATION PROTOCOLS__

Services communicate using established rules that determine data transmission over a network. These rules are called communication protocols. Some standard protocols to implement SOA include the following:

- Simple Object Access Protocol (SOAP)
- RESTful HTTP
- Apache Thrift
- Apache ActiveMQ
- Java Message Service (JMS)

__SOA BENEFITS__

Service-oriented architecture (SOA) has several benefits over the traditional monolithic architectures in which all processes run as a single unit.

1. Faster time to market

Developers reuse services across different business processes to save time and costs. They can assemble applications much faster with SOA than by writing code and performing integrations from scratch.

2. Efficient maintenance

It’s easier to create, update, and debug small services than large code blocks in monolithic applications. Modifying any service in SOA does not impact the overall functionality of the business process.

3. Greater adaptability

SOA is more adaptable to advances in technology. You can modernize your applications efficiently and cost effectively. For example, healthcare organizations can use the functionality of older electronic health record systems in newer cloud-based applications.

__ESB__

An enterprise service bus (ESB) is software that you can use when communicating with a system that has multiple services. It establishes communication between services and service consumers no matter what the technology.

<img src="/content/esb.png">

__SOA DRAWBACKS__

1. Limited scalability

System scalability is significantly impacted when services share many resources and need to coordinate to perform their functionality.

2. Increasing interdependencies

Service-oriented architecture (SOA) systems can become more complex over time and develop several interdependencies between services. They can be hard to modify or debug if several services are calling each other in a loop. Shared resources, such as centralized databases, can also slow down the system.

3. Single point of failure

For SOA implementations with an ESB, the ESB creates a single point of failure. It is a centralized service, which goes against the idea of decentralization that SOA advocates. Clients and services cannot communicate with each other at all if the ESB goes down.

__MICROSERVICES vs SOA__

<img src="/content/microservices.png">

Microservices architecture is made up of very small and completely independent software components, called microservices, that specialize and focus on one task only.

Microservices communicate through APIs, which are rules that developers create to let other software systems communicate with their microservice.

Microservices address the shortcomings of SOA to make the software more compatible with modern cloud-based enterprise environments.

- They are fine grained and favor data duplication as opposed to data sharing.

    - This makes them completely independent with their own communication protocols that are exposed through lightweight APIs.

It’s essentially the consumers' job to use the microservice through its API, thus removing the need for a centralized ESB.

# Cloud Load Balancing

__HORIZONTAL SCALE LOAD BALANCING__

The distribution of loads across as many servers as necessary to handle the workload.

- In this case, you can scale infinitely by adding more physical machines to an existing pool of resources.

<img src="/content/cloud-load-balancers.png">

Load balancers can either be hardware-based or software-based that prevents servers from breaking down or getting overloaded.

- When faced with a sudden surge in requests, your application will load slowly, the network will time out, and your server will creak.

__CLOUD LOAD BALANCING__

Cloud load balancing takes a software-based approach to distributing network traffic across resources, as opposed to hardware-based load balancing, which is more common in enterprise data centers.

- software-based is not an instance-based or device-based solution, so you won't be locked into a physical load-balancing infrastructure or face the HA, scale, and management challenges inherent in instance-based load balancers.

<img src="/content/cloud-load-balancer-functions-2.png">

A load balancer receives incoming traffic and routes those requests to active targets based on a configured policy.

A load balancing service also monitors the health of the individual targets to ensure that those resources  are fully operational.

__BENEFITS__

<img src="/content/cloud-load-balancer-functions-1.jpeg">

Prevents Network Server Overload

- When using load balancers in the cloud, you can distribute your workload among several servers, network units, data centers, and cloud providers.

- This lets you effectively prevent network server overload during traffic surges.

High Availability

- The concept of high availability means that your entire system won’t be shut down whenever a system component goes down or fails.

- You can use load balancers to simply redirect requests to healthy nodes in the event that one fails.

Better Resource Utilization

- Load balancing is centered around the principle of efficiently distributing workloads across data centers and through multiple resources, such as disks, servers, clusters, or computers.

- It maximizes throughput, optimizes the use of available resources, avoids overload of any single resource, and minimizes response time.

Prevent a Single Source of Failure

- Load balancers are able to detect unhealthy nodes in your cluster through various algorithmic and health-checking techniques.

- In the event of failure, loads can be transferred to a different node without affecting your users, affording you the time to address the problem rather than treating it as an emergency.

__FEATURES__

Single anycast IP address

- With Cloud Load Balancing, a single anycast IP address is the frontend for all of your backend instances in regions around the world.

- It provides cross-region load balancing, including automatic multi-region failover, which moves traffic to failover backends if your primary backends become unhealthy.

- Cloud Load Balancing reacts instantaneously to changes in users, traffic, network, backend health, and other related conditions.

Seamless Autoscaling

- Cloud Load Balancing can scale as your users and traffic grow, including easily handling huge, unexpected, and instantaneous spikes by diverting traffic to other regions in the world that can take traffic.

- Autoscaling does not require pre-warming: you can scale from zero to full traffic in a matter of seconds.

Layer 4 and Layer 7 load balancing

- Use Layer 4-based load balancing to direct traffic based on data from network and transport layer protocols such as TCP, UDP, ESP, GRE, ICMP, and ICMPv6 .

- Use Layer 7-based load balancing to add request routing decisions based on attributes, such as the HTTP header and the uniform resource identifier.

External and internal load balancing

- You can use external load balancing when your users reach your applications from the internet and internal load balancing when your clients are inside of Google Cloud.

- Global and regional load balancing. Distribute your load-balanced resources in single or multiple regions, to terminate connections close to your users, and to meet your high availability requirements.

# Memory Management

Memory management is all about making sure there is as much available memory space as possible for new programs, data and processes to execute.

__The Memory Management Unit (MMU)__

<img src="/content/computer_system.png">

Within a computing system is the core hardware component that translates virtual logical address space to physical addresses. The MMU is typically a physical piece of hardware and is sometimes referred to as a Paged Memory Management Unit (PMMU).

- Physical addresses: The physical address is the memory location within system RAM and is identified as a set of digits.

- Logical addresses: Also sometimes referred to as virtual memory, a logical address is what operating systems and applications access to execute code, as an abstraction of physical address space.

As memory is used by multiple parts of a modern system, memory allocation and memory management can take on different forms.

<img src="/content/memory_management.png">

__Operating System__

Operating systems like Microsoft Windows and Linux, can make use of physical RAM as well as hard drive swap space to manage a total pool of available memory.

When memory is allocated in a system, not all of the available is always consumed in a linear manner, which can lead to fragmentation.

- Internal Fragmentation – Memory is allocated to a process or application and isn’t used, leaving un-allocated or fragmented memory.

- External Fragmentation – As memory is allocated and then deallocated, there can be small spaces of memory leftover, leaving memory holes or “fragments” that aren’t suitable for other processes.

__Programming Languages__

The C programming language requires developers to directly manage memory utilization, while other languages like Java and C#, for example, provide automatic memory management.

- Static Loading – Code is loaded into memory, before it is executed. Used in structured programming languages including C.

- Dynamic Loading – Code is loaded into memory as needed. Used in object oriented programming languages, such as Java.

__Applications__

Applications consume and manage memory, but are often limited in memory management capabilities as defined by the underlying language and operating system.

__Storage Memory Management__

With new NVME storage drives, operating systems can benefit from faster storage drives to help expand and enable more persistent forms of memory management.

<img src="/content/cpu.jpeg">

__cpu (central processing unit)__

circuitry in a computer that controls the manipulation of data that powers a computer via a small flat square called the motherboard

<img src="/content/cpu_components.png">

__cpu component: ALU (arithmetic logic unit)__

circuitry that performs operations like addition & subtraction on data

__cpu component: control unit__

controls the ciruitry for coordinating all of the computer's activities

__cpu component: register unit__

which contains temporary memory for data

__volatile main memory/RAM (random access memory)__

temporary holding of software programs and apps and their associated data until the power is turned off

__non-volatile storage memory__

long-term holding of software programs and apps and their associated data even if the power is turned off

ex) memory sticks, hard disk drive, solid state drives(SSD)

# Page Memory & Paging

Paging is a method of writing and reading data from a secondary storage(Drive) for use in primary storage(RAM).

When a computer runs out of RAM, the operating system (OS) will move pages of memory over to the computer’s hard disk to free up RAM for other processes. This ensures that the operating system will never run out of memory and crash.

<img src="/content/paging.png">

When a program tries to access a page that is not stored in RAM, the processor treats this action as a page fault. When this occurs the operating system must:

- Determine the location of the data on disk.

- Obtain an empty page frame in RAM to use as a container for the data.

- Load the requested data into the available page frame.

- Update the page table to refer to the new page frame.

- Return control to the program, transparently retrying the instruction that caused the page fault.

__Translation Lookaside Buffer(TLB)__

The TLB is a memory cache that stores recent translations of virtual memory to physical addresses for faster retrieval.

Every time the OS is translating from logical to physical, it requires a look up in the page table, which is stored in RAM. Meaning every process request would require two physical memory accesses. This issue greatly reduces the overall performance of our equipment.

__Pros:__

By diving the memory into fix blocks, it eliminates the issue of External Fragmentation. It also supports Multiprogramming. Overheads that come with compaction during relocation are eliminated. Easy to swap since everything is the same size, which is usually the same size as disk blocks to and from which pages are swapped.

__Cons:__

Paging increases the price of computer hardware, as page addresses are mapped to hardware. Memory is forced to store variables like page tables. Some memory space stays unused when available blocks are not sufficient for address space for jobs to run. Since the physical memory is split into equal sizes, it allows for internal fragmentation.