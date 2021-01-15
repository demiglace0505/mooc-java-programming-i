## [Part 1 - Basics and Getting Familiar](https://java-programming.mooc.fi/part-1)

> **Important concepts learned**
>
> - printing
>
> - scanner
>
> - conditionals

- [Reading Input](#reading-input)
- [Variables](#variables)
- [Calculating with Numbers](#calculating-with-numbers)
- [Conditional statements and conditional operation](#conditional-statements-and-conditional-operation)

_____

### Reading Input

The Scanner tool that comes with Java can be used to read user input. A scanner is imported and defined as

```
import java.util.Scanner;

Scanner myScanner = new Scanner(System.in);
```

We can read the user's input using the **nextLine()** method of the Scanner object.

```
String message = myScanner.nextLine();
```

### Variables

In this part, variables are introduced to us. There are many types such as String, int, double, boolean. A variable's value can be changed anytime, but it's type persists and can no longer be changed, except for integer which can be converted to double. 

```
int number = 123;
System.out.println("The value of the variable is " + number);

number = 42;
System.out.println("The value of the variable is " + number);
```

For naming variables, camelCase is the preferred way for java.

#### Converting String to Integer 

Converting string to integer is possible with the **Integer.valueOf()** method. The same is true with **Double.valueOf()**

#### Boolean

For boolean values, the string must be "true" (case insensitve) in order for it to be true. All other strings returns false.

### Calculating with Numbers

It is important to note that if one of the operands is a string, the other operand will also be changed to a string too. 

```
System.out.println("Four: " + (2 + 2));  -------> Four: 4
System.out.println("But! Twenty-two: " + 2 + 2); ------> But! Twenty-two: 22
```

Addition, Subtraction, and Multiplication are pretty straightforward in Java. Division, on the other hand is a little trickier since if all values in the expression are integers, the result will also be an integer. But if one or  both is a float type, the answer will be a float type.

#### Converting integer to float

Integers can be converted to float using **(double)** or by multiplying it with **1.0**

```
int first = 3;
int second = 2;

double result1 = (double) first / second;
System.out.println(result1); // prints 1.5
```

### Conditional statements and conditional operation

In this segment, I learned about conditional statements like if, else, else if

```
if () {

} else {

}
```

I also learned of conditional operators like and **&&** or **||** and not **!**