__Q1__

Given a signed 32-bit integer x, return x with its digits reversed

- if reversing x causes it to go outside the signed 32-bit integer range, return 0

- assume env does not allow 64-bit integers

TIME COMPLEXITY
O(1) linear: dependent length of n

SPACE COMPLEXITY
O(1) constant: in-place algorithm that doesn't require additional memory space

```json

public int reversed(int x) {

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

private int recursion(int x, int result) {

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

```json

public ArrayList<String> fizzBuzz(long number) {

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