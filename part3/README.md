## [Part 3 - List and Array](https://java-programming.mooc.fi/part-3)

> **Important concepts learned**
>
> - Iterating through a list
>
>
> - Removing and checking values in a list
>
>
> - Declaring Arrays
>- String methods
> - Splitting csv

- [Lists](#lists)
- [Arrays](#arrays)
- [Using strings](#using-strings)

_____

### Lists

The [Array List](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html) is a pre-made, very useful tool for dealing with lists. To create a list, it is first imported. Then it is created with the command `ArrayList<Type> list = new ArrayList<>()`, where type is the type of value to be stored. All the variables stored in the list is of the same type. The variables in an array list are all of reference-type, not primitive type. 

```
import java.util.ArrayList;

public class Program {

    public static void main(String[] args) {
        // create a list
        ArrayList<String> list = new ArrayList<>();

    }
}
```

#### Adding and Retrieving from a list

Adding an item to the list is done with the **add()** method. **get(index)**, on the other hand, retrieves a value from a certain position.

#### Iterating over a list

We can use a loop and ArrayList's **.size()** method to iterate over a list.

```
ArrayList<String> teachers = new ArrayList<>();

teachers.add("Simon");
teachers.add("Samuel");
teachers.add("Ann");
teachers.add("Anna");

for (int index = 0; index < teachers.size(); index++) {
    System.out.println(teachers.get(index));
}
```

#### Iterating over a list using for-each loop

Instead of using Array size and index for iterating, we can make use of for-each loop. The syntax is `for (<type> <item>: <array>)`

```
ArrayList<String> teachers = new ArrayList<>();

teachers.add("Simon");
teachers.add("Samuel");
teachers.add("Ann");
teachers.add("Anna");

for (String teacher: teachers) {
    System.out.println(teacher);
}
```

#### Removing from a list

An item can be removed form the list using the **remove(index)** method. We can also remove a specific item

```
ArrayList<String> list = new ArrayList<>();

list.add("First");
list.add("Second");
list.add("Third");

list.remove("First");

System.out.println("Index 0 so the first value: " + list.get(0));
System.out.println("Index 1 so the second value: " + list.get(1));

//OUTPUT:
Index 0 so the first value: Second
Index 1 so the second value: Third
```

To remove an integer, **Integer.valueOf()** method has to be used.

```
ArrayList<Integer> list = new ArrayList<>();

list.add(15);
list.add(18);
list.add(21);
list.add(24);

list.remove(2);
list.remove(Integer.valueOf(15));

System.out.println("Index 0 so the first value: " + list.get(0));
System.out.println("Index 1 so the second value: " + list.get(1));

//OUTPUT:
Index 0 so the first value: 18
Index 1 so the second value: 24
```

#### Checking for a value in a list

The list method **contains()** can be used to search for a value. It returns boolean true when it finds the value, false if otherwise.

#### List as a method parameter

A list can also be used as a parameter for a method. The type of parameter is defined as the type of the list and the type of values contained in that list. The method print below prints all the values in a list.

```
public static void print(ArrayList<String> list) {
    for (String value: list) {
        System.out.println(value);
    }
}
```

### Arrays

The array is the ancestor of the ArrayList. There are two ways to create an array. An array is declared by adding square brackets after the type of element. In this case, the array numbers can hold 3 integers.

```
int[] numbers = new int[3];
```

Another way to create an array is by this syntax:

```
int[] numbers = {100, 1, 42};
```

### Using Strings

To compare strings, the **equals()** method is used.

```
String text = "course";
String anotherText = "horse";

if (text.equals(anotherText)) {
    System.out.println("The two texts are equal!");
} else {
    System.out.println("The two texts are not equal!");
}
```

A string can be splitted using the **split()** method, which takes a parameter where the string should be split. Splitting a string always returns an array of strings.

```
String text = "first second third fourth";
String[] pieces = text.split(" ");

for (int i = 0; i < pieces.length; i++) {
    System.out.println(pieces[i]);
}
```

Should output

```
first
second
third
fourth
```

We can search for a substring using the **contains()** method.

```
String text = "volcanologist";

if (text.contains("can")) {
    System.out.println("can was found");
}

//can was found
```

We can also get a character at a specified index using the **charAt()** method, and we can get the length of the string using the **length()** method.