## [Part 6 - Object Oriented Programming cont.](https://java-programming.mooc.fi/part-6)

> **Important concepts learned**
>
> - Objects in an object
> - Testing

- [Objects that contain a list](#objects-that-contain-a-list)
- [Retrieving a specific object  from a list](#retrieving-a-specific-object-from-a-list)
- [Separating User Interface from program logic](#separating-user-interface-from-program-logic)
- [Testing](#testing)

_____

### Objects that contain a list

```
public class Playlist {
    private ArrayList<String> songs;

    public Playlist() {
        this.songs = new ArrayList<>();
    }

    public void addSong(String song) {
        this.songs.add(song);
    }

    public void removeSong(String song) {
        this.songs.remove(song);
    }

    public void printSongs() {
        for (String song: this.songs) {
            System.out.println(song);
        }
    }
}
```

### Retrieving a Specific Object from a list

The example below retrieves the tallest person from the list. First we check if the list is empty, and if it is, return null.

```
public Person getTallest() {
    // return a null reference if there's no one on the ride
    if (this.riding.isEmpty()) {
        return null;
    }

    // create an object reference for the object to be returned
    // its first value is the first object on the list
    Person returnObject = this.riding.get(0);

    // go through the list
    for (Person prs: this.riding) {
        // compare each object on the list
        // to the returnObject -- we compare heights
        // since we're searching for the tallest,

        if (returnObject.getHeight() < prs.getHeight()) {
            // if we find a taller person in the comparison,
            // we assign it as the value of the returnObject
            returnObject = prs;
        }
    }

    // finally, the object reference describing the
    // return object is returned
    return returnObject;
}
```

### Separating the User Interface from program logic

We can do this by implementing a User Interface class that takes a scanner object for reading input.

```
public class UserInterface {
    private Scanner scanner;

    public UserInterface(Scanner scanner) {
        this.scanner = scanner;
    }

    public void start() {
        // do something
    }
}
```

Creating an instance of the user interface can be done so:

```
public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    UserInterface userInterface = new UserInterface(scanner);
    userInterface.start();
}
```

### Testing

#### Passing test input to scanner

```
String input = "one\n" + "two\n"  +
                "three\n" + "four\n" +
                "five\n" + "one\n"  +
                "six\n";

Scanner reader = new Scanner(input);

ArrayList<String> read = new ArrayList<>();

while (true) {
    System.out.println("Enter an input: ");
    String line = reader.nextLine();
    if (read.contains(line)) {
        break;
    }

    read.add(line);
}

System.out.println("Thank you!");

if (read.contains("six")) {
    System.out.println("A value that should not have been added to the group was added to it.");
}
```

#### Unit Testing

Unit testing refers to the testing of individual components. The test classes are created under the Test-Packages folder. The most common testing library in Java is [JUnit](http://junit.org/). The class name is to be affixed with **Test**, in order for the IDE to recognize that it is a test class. Also, each test method should have the annotation `@Test`.

The example below tests that the new calculator object created has an initial value of 0.

```
import static org.junit.Assert.assertEquals;
import org.junit.Test;

public class CalculatorTest {

    @Test
    public void calculatorInitialValueZero() {
        Calculator calculator = new Calculator();
        assertEquals(0, calculator.getValue());
    }

    @Test
    public void valueFiveWhenFiveAdded() {
        Calculator calculator = new Calculator();
        calculator.add(5);
        assertEquals(5, calculator.getValue());
    }

    @Test
    public void valueMinusTwoWhenTwoSubstracted() {
        Calculator calculator = new Calculator();
        calculator.subtract(2);
        assertEquals(-2, calculator.getValue());
    }
}
```

#### Test-Driven Development

In test-driven development, the functionality of the program is constructed in small steps. A programmer first writes an automatically-executable test, which tests a single piece of the computer program. The five steps of test-driven software development are:

1. Writing a test
2. Running the tests - at this stage, the test should fail since the functionality has not yet been implemented.
3. Write the functionality that meets the test requirements
4. Perform tests
5. Repair/refactor the structure of the program

Overall, the advantages are:

- Forces thinking of functionality before writing code
- Maintainable structure due to small modular parts
- The end product contains tests
- Lesser bugs