## [Part 5 - Object Oriented Programming cont.](https://java-programming.mooc.fi/part-5)

> **Important concepts learned**
>
> - Constructor and method overloading
> - Comparing object equality, including lists

- [Overloading Constructors](#overloading-constructors)
- [Method Overloading](#method-overloading)
- [Primitive and Reference variables](#primitive-and-reference-variables)
- [Objects and References](#objects-and-references)
- [Comparing Object equality using equals](#comparing-object-equality-using-equals)
- [Object equality and lists](#object-equality-and-lists)

_____

### Overloading Constructors

Constructor Overloading is the technique of having two or more constructors in a class. By having an alternative constructor, there are now two ways to create an object. A constructor can call another constructor.

```
public Person(String name, int age) {
    this.name = name;
    this.age = age;
    this.weight = 0;
    this.height = 0;
}

public Person(String name) {
    this(name,0);
}

/////////
public static void main(String[] args) {
    Person paul = new Person("Paul", 24);
    Person ada = new Person("Ada");
```

### Method Overloading

```
public void growOlder() {
    this.age = this.age + 1;
}

public void growOlder(int years) {
    this.age = this.age + years;
}
```

### Primitive and reference variables

#### Primitive Variable

Variable information is stored as the value of that variable. Primitive variables usually are immutable. The eight primitive variables are:

| primitive variable | description                                                  |
| ------------------ | ------------------------------------------------------------ |
| boolean            | true or false                                                |
| byte               | 8 bits between -128 and 127                                  |
| char               | 16 bit value representing a single character                 |
| short              | 16 bit value representing a small integer between -32768 and 32767 |
| int                | 32 bit value between -2^31 and 2^31-1                        |
| long               | 64 bit value between -2^63 and 2^63-1                        |
| float              | floating point 32 bits                                       |
| double             | floating point 64 bits                                       |

#### Reference Variable

Holds reference to information related to a variable. Typically always objects in java. Reference variables can typically mutated because the value of a primitive variable is stored directly in the variable, whereas the value of a reference variable is a reference to a variable's data (internal state).

### Objects and References

A constructor  call returns a reference to an object, which is the information about the location of object data. Assigning a reference type variable copies the reference in this scenario `Person ball = joan;`. Printing a null reference prints "null". Calling a method on a null reference would give us Null Pointer Exception.

```
Person joan = new Person("Joan Ball");
System.out.println(joan);

Person ball = joan;
ball.growOlder();
ball.growOlder();

System.out.println(joan);

joan = new Person("Joan B.");
System.out.println(joan);

ball = null;
System.out.println(ball);

ball.growOlder(); ---> Null Pointer Exception

//OUTPUT:
Joan Ball, age 0 years
Joan Ball, age 2 years
Joan B., age 0 years
null
```

### Object of same type as method parameter

In object oriented programming, abstraction is one of the principles. We created a SimpleDate class and a **before()** method to compare dates.

```
public class SimpleDate {
    private int day;
    private int month;
    private int year;
    
    //...
        public boolean before(SimpleDate compared){
        if (this.year < compared.year) {
            return true;
        }
        if (this.year > compared.year) {
            return false;
        }
//        same year, compare months
        if (this.month < compared.month) {
            return true;
        }
        if (this.month > compared.month) {
            return false;
        }
//        compare days
        if (this.day < compared.day) {
            return true;
        }
        return false;
}
```

The method **before()** of the SimpleDate Class can then be used after getting a Person's `birthday`.

```
public class Person {

    private String name;
    private SimpleDate birthday;
    
    //...
        public boolean olderThan(Person compared) {
        if (this.birthday.before(compared.getBirthday())) {
            return true;
        }
        return false;
    }
```

### Comparing object equality using equals

With primitive variables such as `int`, comparing variables can be done using two equals sign (==). For reference variables, equals compares the reference to the memory location. 

```
SimpleDate first = new SimpleDate(1, 1, 2000);
SimpleDate second = new SimpleDate(1, 1, 2000);
SimpleDate third = new SimpleDate(12, 12, 2012);
SimpleDate fourth = first;

if (first.equals(first)) {
    System.out.println("Variables first and first are equal");
} else {
    System.out.println("Variables first and first are not equal");
}

...


///OUTPUT:
Variables first and first are equal
Variables first and second are not equal
Variables first and third are not equal
Variables first and fourth are equal
```

We can define our own equals method that compares values properly. Since all objects are `Object` type in addition to its own type, the **equals()** method receives an `Object` type object.

```
public class Person {

    private String name;
    private int age;
    private int weight;
    private int height;

    // constructors and methods


    public boolean equals(Object compared) {
        // if the variables are located in the same position, they are equal
        if (this == compared) {
            return true;
        }

        // if the compared object is not of type Person, the objects are not equal
        if (!(compared instanceof Person)) {
            return false;
        }

        // convert the object into a Person object
        Person comparedPerson = (Person) compared;

        // if the values of the object variables are equal, the objects are equal
        if (this.name.equals(comparedPerson.name) &&
            this.age == comparedPerson.age &&
            this.weight == comparedPerson.weight &&
            this.height == comparedPerson.height) {
            return true;
        }

        // otherwise the objects are not equal
        return false;
    }

}
```

### Object equality and lists

The **contains** method of a list uses the **equals** method to search for objects. An object with a different reference but exact same contents will not be found in the list. To solve this, we can implement our own **equals** method. With this, the contains method will now recognize Birds with identical contents.

```
public class Bird {
    private String name;

    public Bird(String name) {
        this.name = name;
    }

    public boolean equals(Object compared) {
        // if the variables are located in the same position, they are equal
        if (this == compared) {
            return true;
        }

        // if the compared object is not of type Bird, the objects are not equal
        if (!(compared instanceof Bird)) {
            return false;
        }

        // convert the object to a Bird object
        Bird comparedBird = (Bird) compared;

        // if the values of the object variables are equal, the objects are, too
        return this.name.equals(comparedBird.name);

        /*
        // the comparison of names above is equal to
        // the following code

        if (this.name.equals(comparedBird.name)) {
            return true;
        }

        // otherwise the objects are not equal
        return false;
        */
    }
}
```

