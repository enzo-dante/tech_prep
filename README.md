# Big O Notation

ALGORITHM: repeatable sequence of steps

TIME COMPLEXITY: independent of hardware, the worst-case number of steps required for an algorithm to perform successfully.

SPACE COMPLEXITY: the total memory space required by the algorithm's input size plus the extra space or temporary space used by an algorithm (AUXILIARY SPACE).

### Big O Types (best-to-worst)

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

SERIALIZATION: the conversion of a Java object into a static stream (sequence) of bytes, which we can then save to a database or transfer over a network.

The serialization process is instance-independent; classes that are eligible for serialization need to implement Serializable interface.

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

serialize & deserialize

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
     * Call the ObjectInputStream() reads a stream of bytes and converts it back into a Java object. It can then be cast back to the original object.
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


# Recursion

RECURSIVE FUNCTIONS: a continuously self-calling algorithm & each call on the call-stack waits for the algorithm to reach a base case/breaking condition for a return value.

```
recursive factorial method

    !3 = 1*2*3 = 6

        recursiveFactorial(3)
                returns 3 * (2 * 1) = 6

        recursiveFactorial(2)
                returns 2 * 1

        recursiveFactorial(1)
                returns 1 * 1

        recursiveFactorial(0)
                returns 1
```

RECURSIVE BASE CASE: the breaking condition that initiates an upward propogation of return of values for the waiting calls that results in a call-stack resolution or overflow

```
private static int recursiveFactorial(int n) {

    boolean isBaseCase = (n == 0);

    if(isBaseCase) return 1;

    System.out.println("factorial: " + n)

    return recursiveFactorial(n - 1) * n;

}
```

# Data Structures 

### arrays

O(1) CONSTANT time complexity when getting an element in an array with an index

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

null --> HEAD <--> { currentNodeValue, nextNodePointer } <--> { currentNodeValue, nextNodePointer } <--> TAIL --> null

```
public class DoublyLinkedList {

    private Employee head;
    private Employee tail;
    private int size;

    public DoublyLinkedList() {
        this.head = null;
        this.tail = null;
        this.size = null;
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
        EmployeeNode node = new EmployeeNode(employee);

        if(isEmpty()) {

            // if the linkedList is empty, than added node will serve as head and tail
            this.tail = node;

        } else {

            // If list is NOT empty, set the current head node's doubly previous pointer to the new node. 
            this.head.setPrevious(node);

            // set the current head as the new node's next value (shift current head down 1 node)
            node.setNext(this.head);
        }

        // establish new doubly-linked node as new head
        this.head = node;
        this.size++;
    }

    /**
     * O(1) CONSTANT time complexity when adding node to the front of a list since index will always be last
     * O(n) LINEAR space complexity when adding node to a list to account for new field in memory 
     */
    public void addToEnd(Employee employee) {

        // instantiate a new node that will serve as the new head of the linkedList
        EmployeeNode node = new EmployeeNode(employee);

        if(isEmpty()) {

            // if the linkedList is empty, than added node will serve as head and tail
            this.head = node;

        } else {

            // If list is NOT empty, set the current tail node's doubly next pointer to the new node. 
            this.tail.setNext(node);

            // set the current tail as the new node's previous value (shift current tail up 1 node)
            node.setPrevious(this.tail);
        }

        // establish new doubly-linked node as new tail
        this.tail = node;
        this.size++;
    }

    /**
     * O(1) CONSTANT time complexity when removing node to the front of a list since index will always be 0
     * O(1) CONSTANT space complexity when removing node from a list 
     */
    public EmployeeNode removeFromFront() {

        if(isEmpty()) return null;

        EmployeeNode removedNode = this.head;

        if(this.head.getNext() == null) {

            // if linkedList only has 1 node, set tail to null to facilitate linkedList emptiness 
            this.tail = null;

        } else {

            // if linkedList has more than 1 node, set current head's nextNode previous pointer to null
            this.head.getNext().setPrevious(null);
        }

        // establish new head
        this.head = this.head.getNext();
        this.size--;

        removedNode.setNext(null);
        return removedNode;
    }

    /**
     * O(1) CONSTANT time complexity when removing node to the front of a list since index will always be 0
     * O(1) CONSTANT space complexity when removing node from a list 
     */
    public EmployeeNode removeFromEnd() {

        if(isEmpty()) return null;

        EmployeeNode removedNode = this.tail;

        if(this.tail.getPrevious() == null) {

            // if linkedList only has 1 node, set head to null to facilitate linkedList emptiness 
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