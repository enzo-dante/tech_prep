__Q1__

Given a signed 32-bit integer x, return x with its digits reversed

- if reversing x causes it to go outside the signed 32-bit integer range, return 0

- assume env does not allow 64-bit integers

TIME COMPLEXITY
O(1) linear: dependent length of n

SPACE COMPLEXITY
O(1) constant: in-place algorithm that doesn't require additional memory space

```json

@Test
void reversed_positiveInput() {
    int input = 123;

    int expected = 321;
    int actual = Q1.reversed(input);
    assertEquals(expected, actual);
}

@Test
void reversed_negativeInput() {
    int testInput = -123;

    int expected = -321;
    int actual = Q1.reversed(input);
    assertEquals(expected, actual);
}

public static int reversed(int x) {

    boolean isNegative = false;
    int result = 0;

    if(x < 0) {
        x *= -1;
        isNegative = true;
    }

    result = recursion(x, result);

    if(isNegative) result *= -1;

    return result;
}

private static int recursion(int x, int result) {

    boolean isBaseCase = (x <= 0);

    if(isBaseCase) return 0;

    int lastDigit = x % 10;

    x /= 10;
    result = (result * 10) + lastDigit;

    return recursion(x, result);
}
```

__Q2__

write a program that outputs the string representation of a long number from 1 to n

- the method returns an arrayList of GENERIC CLASS strings

for multiples of:
- 3 it should return "Fizz" instead of the number
- 5 it should return "Buzz" instead of the number
- 5 AND 3 it should return "FizzBuzz" instead of the number

TIME COMPLEXITY
O(n) linear: dependent length of n

SPACE COMPLEXITY
O(1) constant: in-place algorithm that doesn't require additional memory space

```json

private static final String FIZZ = "Fizz"; 
private static final String BUZZ = "Buzz"; 
private static final String FIZZ_BUZZ = "FizzBuzz"; 

@Test
void fizzBuzz_0() {
    ArrayList<String> actualValues = Q2.fizzBuzz(-3);
    assertEquals(null, actualValues);
}

@Test
void fizzBuzz_3() {
    ArrayList<String> actualValues = Q2.fizzBuzz(3);
    ArrayList<String> expectedValues = new ArrayList<>();

    expectedValues.add("1");
    expectedValues.add("2");
    expectedValues.add(FIZZ);

    assertEquals(expectedValues, actualValues);
}

@Test
void fizzBuzz_5() {
    ArrayList<String> actualValues = Q2.fizzBuzz(5);
    ArrayList<String> expectedValues = new ArrayList<>();

    expectedValues.add("1");
    expectedValues.add("2");
    expectedValues.add(FIZZ);
    expectedValues.add("4");
    expectedValues.add(BUZZ);

    assertEquals(expectedValues, actualValues);
}

@Test
void fizzBuzz_3And5() {
    ArrayList<String> actualValues = Q2.fizzBuzz(15);
    ArrayList<String> expectedValues = new ArrayList<>();
    
    expectedValues.add("1");
    expectedValues.add("2");
    expectedValues.add(FIZZ);
    expectedValues.add("4");
    expectedValues.add(BUZZ);

    expectedValues.add(FIZZ);
    expectedValues.add("7");
    expectedValues.add("8");
    expectedValues.add(FIZZ);
    expectedValues.add(BUZZ);

    expectedValues.add("11");
    expectedValues.add(FIZZ);
    expectedValues.add("13");
    expectedValues.add("14");
    expectedValues.add(FIZZ_BUZZ);

    assertEquals(expectedValues, actualValues);
}

public static ArrayList<String> fizzBuzz(long number) {

    if(number < 1) return null;

    ArrayList<String> strings = new ArrayList<>();
    int i;

    while(i <= number) {

        boolean divBy5 = (i % 5 == 0);
        boolean divBy3 = (i % 3 == 0);

        if(divBy5 && divBy3) {

            strings.add("FizzBuzz");

        } else if(divBy3) {

            strings.add("Fizz");

        } else if(divBy5) {

            strings.add("Buzz");

        } else {
            strings.add(Long.toStrings(i));
        }

        i++;
    }

    return strings;
}
```

__Q3__

Given a square matrix mat, return the sum of the matrix diagonals.

- only include the sum of all the elements on the primary diagonal

- all the elements on the secondary diagonal that are not part of the primary diagonal.

Logic:

     length = width or height

     diagonal_1 = 1 + 5 + 9 = 15 = matrix[i][i]

     diagonal_2 = 3 + 5 + 7 = 15 = matrix[i][length - i - 1]

     matrix = [
           [1,2,3],
           [4,5,6],
           [7,8,9]
     ]

     remove duplicate 5 that appears in both diagonals from current sum 30
     diagonal_sum = 25

     step 1a: define index of traversing row
     step 1b: define index of shifting diagonal

     step 2: add to sum

     step 3: iterate over rows repeating process

     step 4: remove duplicate middle element from sum if matrix length is odd

     step 5: return sum

TIME COMPLEXITY
O(n) linear: where n is the length of the given array

SPACE COMPLEXITY
O(1) constant: in-place algorithm that doesn't require additional memory space

```json

@Test
void matrixDiagonalSum_success() {

    int[][] test = {
            {1,2,3},
            {4,5,6},
            {7,8,9}
    };

    int expected = 25;
    int actual = Q3.matrixDiagonalSum(test);
    assertEquals(expected, actual);
}

@test
matrixDiagonalSum_fail_badInput() {

    int[][] input = null;

    int expected = -1;
    int actual = Q3.matrixDiagonalSum(input);
    assertEquals(expected, actual);
}

public static int matrixDiagonalSum(int[][] matrix) {

    if(matrix == null || matrix.length == 0) return -1;

    int sum;

    // traverse rows
    for(int row = 0; row < matrix.length; row++) {

        // start index of second diagonal
        int diagonal = (matrix.length - 1) - row;

        int valueD1 = matrix[row][row];
        int valueD2 = matrix[row][diagonal];

        sum += (valueD1 + valueD2);
    }

    // remove duplicate middle element
    boolean isOddMatrixLength = (matrix.length % 2 != 0);

    if(isOddMatrixLength) {

        int middleIndex = matrix.length / 2;
        int middleValue = matrix[middleIndex][middleIndex];

        return sum - middleValue;
    }

    return sum;
}
```

__Q4__

Given an array of non-negative integers arr, you are initially positioned at start index of the array.

- When you are at index i, you can jump to:

```json

(i + arr[i]) || (i - arr[i])
```

- check if you can reach to any index with value 0.

- Notice that you can not jump outside the array at any time.

Logic:

- use Depth First Search (DFS) by using recursive functions calls for incrementing & decrementing start parameters
- its DFS because the method will handle one direction first and drill down for a base case
- before continuing to next recursive direction if necessary

DEPTH FIRST SEARCH: recursively, check if the currentNode has any children (left-to-right) that has the search path for the target node

- hasPath(s, t): recursively, nodeS do you have a path to nodeT?
- nodeS asks (left-to-right) it's child if it has a path to nodeT, repeat until reached nodeT or null

TIME COMPLEXITY
O(n) linear: worst-case, traverse the length of the input array size

SPACE COMPLEXITY
O(1) constant SPACE COMPLEXITY: in-place algorithm that doesn't require additional memory space

```json

@Test
jumpGame3_true() {

    int[] input = {4,2,3,0,3,1,2};
    int start = 5;
    boolean actual = Q4.jumpGame3(input, start);
    assertTrue(actual);
}

@Test
jumpGame3_fail_badInput() {

    int[] array = {};
    int start = -1;

    boolean actual = Q4.jumpGame3(array, start);
    assertFalse(actual);
}

public static boolean jumpGame3(int[] array, int start) {

    if(array.length == 0||
        start < 0 ||
        start >= (array.length - 1)
    ) return false;

    int currentElement = array[start];

    boolean isBaseCase = (currentElement == 0);

    if(isBaseCase) return true;

    int incrementedStart = start + currentElement;
    int decrementedStart = start - currentElement;

    // depth-first search
    return jumpGame3(array, incrementedStart) ||
        jumpGame3(array, decrementedStart);
}
```
