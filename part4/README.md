## [Part 4 - Object Oriented Programming](https://java-programming.mooc.fi/part-4)

> **Important concepts learned**
>
> - Classes and constructor and methods
> - toString string representation
> - Iterating through objects
> - Reading a csv file

- [Object oriented programming](#object-oriented-programming)
- [Objects in a list](#objects-in-a-list)
- [Files and reading data](#files-and-reading-data)

_____

### Object oriented programming

#### Object

An object is an independent entity that contains both data (instance variables) and behavior (methods). Objects hide their internal operations and provides access to its functionality through clearly defined methods. Objects are created from the class through the **new** command.

```
Type varName = new Type(params)
```



#### Class

A class defines the attributes of objects such as: the instance variables (information) and their methods (commands). Instance variables are variables defined inside a class and also called object fields. A class serves as a blueprint for an object. 

```
public class Person {
    private String name;   ----> instance variables
    private int age;
}
```

#### Method

A method is a piece of code written inside a class and is often used to modify the internal state of an object instantiated from a class.

#### Constructor

To construct a class, use the **new** keyword:

```
Person varName = new Person();
```

We can also set an initial state for the object created by defining the constructor method and passing into it a parameter. Note that the constructor name is always the same as the class name (Person)

```
Person ada = new Person("Ada");
```

```
public class Person {
    private String name;
    private int age;

    public Person(String initialName) {
        this.age = 0;
        this.name = initialName;
    }
}
```

#### Defining Methods for an Object

The method for an object is written beneath the constructor. It must be public since it is intended to be visible outside.

```
public class Person {
    private String name;
    private int age;

    public Person(String initialName) {
        this.age = 0;
        this.name = initialName;
    }

    public void printPerson() {
        System.out.println(this.name + ", age " + this.age + " years");
    }
}
```

#### Drawing a diagram

This can be drawn in a class diagram: The variables associated are defined as `variableName: variableType`. The (-) sign means that the variable is encapsulated (private). Since the method printPerson() has a public modifier, it comes with the (+) sign. The method does not return a value, so it has the suffix `void`.

```
________________________________
|  Person                      |
|------------------------------|
| -name:String                 |
| -age:int                     |
-------------------------------|
| +Person(initialName:String)  |
| +printPerson():void          |
|------------------------------|
```

#### Static Methods

The static modifier means that the method does not belong to an object and thus cannot be used to access any variables that belongs to objects.

#### toString Method

The method returning the string representation is toString. 

```
public class Person {
    // ...

    public String toString() {
        return this.name + ", age " + this.age + " years";
    }
}
```

It can be called like this. System.out.println returns the object's string representation. Java automatically extends the call to System.out.println(var.toString())

```
public static void main(String[] args) {
    Person antti = new Person("Antti");
    antti.growOlder();
    
    System.out.println(antti); // same as System.out.println(antti.toString());
}
```

### Objects in a list

We can iterate through objects in a list in 3 ways: a while loop, for loop, and for each.

```
ArrayList<String> names = new ArrayList<>();

// 1. while loop
int index = 0;
while (index < names.size()) {
    System.out.println(names.get(index));
    index = index + 1;
}

// 2. for loop with index
for (int i = 0; i < names.size(); i++) {
    System.out.println(names.get(i));
}

System.out.println();
// 3. for each loop (no index)
for (String name: names) {
    System.out.println(name);
}
```

#### Adding user-inputted objects to a list

We can add to the list using the **add()** method of ArrayList.

```
Scanner scanner = new Scanner(System.in);
ArrayList<Person> persons = new ArrayList<>();

// Read the names of persons from the user
while (true) {
    System.out.print("Enter a name, empty will stop: ");
    String name = scanner.nextLine();
    if (name.isEmpty()) {
        break;
    }

    // Add to the list a new person
    persons.add(new Person(name));
```

#### Filtering out from a list

```
System.out.print("What is the age limit? ");
int ageLimit = Integer.valueOf(scanner.nextLine());

for (Person person: persons) {
    if (person.getAge() >= ageLimit) {
        System.out.println(person);
    }
}
```

### Files and Reading Data

To read a file, the file path is given as a parameter to the constructor of the scanner object. It can be obtained using the **Paths.get** command. The file is read from the project root by default, which is the folder that contains the src folder and pom.xml.

```
import java.util.Scanner;
import java.nio.file.Paths;

try (Scanner scanner = new Scanner(Paths.get("file.txt"))) {

    // we read the file until all lines have been read
    while (scanner.hasNextLine()) {
        // we read one line
        String row = scanner.nextLine();
        // we print the line that we read
        System.out.println(row);
    }
} catch (Exception e) {
    System.out.println("Error: " + e.getMessage());
}
```

Reading a line is done by the **nextLine()** method of the scanner. Skipping an empty line can be done using the command **continue** and **isEmpty()**.

```
// we create a scanner for reading the file
try (Scanner scanner = new Scanner(Paths.get("henkilot.csv"))) {

    // we read all the lines of the file
    while (scanner.hasNextLine()) {
        String line = scanner.nextLine();

        // if the line is blank we do nothing
        if (line.isEmpty()) {
            continue;
        }
        
        // do something with the data

    }
} catch (Exception e) {
    System.out.println("Error: " + e.getMessage());
}
```

#### Reading a csv file

Assuming a class `Person` with instance variables name and age:

```
ArrayList<Person> people = new ArrayList<>();

try (Scanner scanner = new Scanner(Paths.get("records.txt"))) {

    while (scanner.hasNextLine()) {
        String line = scanner.nextLine();

        String[] parts = line.split(",");
        String name = parts[0];
        int age = Integer.valueOf(parts[1]);

        people.add(new Person(name, age));
    }
}
```

