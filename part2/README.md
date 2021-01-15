## [Part 2 - Modular Code](https://java-programming.mooc.fi/part-2)

> **Important concepts learned**
>
> - loops
>
> - methods
>
> - call stack

- [Repeating functionality](#repeating functionality)
- [More loops](#more-loops)
- [Methods and dividing the program into smaller parts](#methods-and-dividing-the-program-into-smaller-parts)

___

### Repeating functionality

In this section, while (true) loops was the main focus. Ending a loop can be caused by the **break** command. Likewise, when we **return** a value from the loop, the loop ends. We can also return to the start of the loop with the **continue** command. Chaining if else if was also tackled in this part.

### More loops

In this section, while loops with a condition and also for loops was introduced.

```
int i = 0;
while (i < 10) {
    System.out.println(i);
    i++;
}
```

```
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}
```

### Methods and dividing the program into smaller parts

#### Method

A method is a statement that can be called from elsewhere in the program. The method is written outside of the main method. Methods are also named in a camelCase syntax.

```
import java.util.Scanner;

public class Example {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // program code
    }

    // your own methods here
    public static void greet() {
        System.out.println("Greetings from the method world!");
    }
}
```

#### Parameters

Parameters are values given to methods to be used in its execution.

```
public static void greet(int numOfTimes) {
    int i = 0;
    while (i < numOfTimes) {
        System.out.println("Greetings!");
        i++;
    }
}
```

Calling `greet(3)` will call the method three times.

A method can also have multiple parameters

```
public static void sum(int first, int second) {
    System.out.println("The sum of numbers " + first + " and " + second + " is " + (first + second));
}
```

To call:

```
sum(3, 5);
```

#### Method return value

The return value for a method is in its definition. Void means no return value.

```
public static **void** incrementByThree() {
    ...
}
```

In cases where the method has return value of void, the execution of the method can be stopped using return alone.

#### Variables Inside Methods

Variables defined inside methods are only visible in that method. The program below prints out 13.

```
public static void main(String[] args) {
    int number = 3;
    modifyNumber(number);
    System.out.println(addAndReturn(number));
}

public static void modifyNumber(int number) {
    number = number + 2;
}

public static int addAndReturn(int number) {
    return number + 10;
}
```

#### Calling a method from another method

This is a multiplication table generator. The rows are printed using the printMultiplicationTableRow() method.

```
public static void multiplicationTable(int max) {
    int number = 1;

    while (number <= max) {
        printMultiplicationTableRow(number, max);
        number++;
    }
}

public static void printMultiplicationTableRow(int number, int coefficient) {

    int printable = number;
    while (printable <= number * coefficient) {
        System.out.print("  " + printable);
        printable += number;
    }

    System.out.println("");
}
```

The output of method call multiplicationTable(3) should be:

```
  1  2  3
  2  4  6
  3  6  9
```

