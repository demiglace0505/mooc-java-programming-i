## [Part 7 - Programming Paradigms and Algorithms](https://java-programming.mooc.fi/part-7)

> **Important concepts learned**
>
> - OOP vs Procedural programming
> - Sorting algorithms
> - Linear and binary searching

- [Programming Paradigms](#programming-paradigms)
- [Sorting an Array and Lists](#sorting-an-array-and-lists)
- [Linear Searching](#linear-searching)
- [Binary Searching](#binary-searching)

_____

### Programming Paradigms

It is a way of thinking about and structuring a program's functionality.

#### Object-Oriented Programming

In OOP, classes define the methods that determine how information is handled. The program is built from small, clear and cooperative entities.

#### Procedural Programming

In Procedural programming, the structure of the program is formed by the functionality desired for the program. The program acts as a step-by-step guide for the functionality to be performed. The state of the program is maintained in variables and tables.

### Sorting an Array and Lists

Here is a sample collection of methods useful for sorting an array according to value.

```
    public static int indexOfSmallestFrom(int[] intArray, int startIndex) {
        int smallestInt = intArray[startIndex];
        int smallestIndex = startIndex;
        for (int i = startIndex; i < intArray.length; i++) {
            if (smallestInt > intArray[i]) {
                smallestInt = intArray[i];
                smallestIndex = i;
            }
        }
        return smallestIndex;
    }
    
    public static void swap (int[] intArray, int first, int second) {
        int indexSwapper = intArray[first];
        intArray[first] = intArray[second];
        intArray[second] = indexSwapper;
    }
    
    public static void sort (int[] intArray){
        int indexHolder = 0;
        System.out.println(Arrays.toString(intArray));
        for (int i = 0; i < intArray.length ; i++) {
            indexHolder = indexOfSmallestFrom(intArray,i);
            swap(intArray, i, indexHolder);
            System.out.println(Arrays.toString(intArray));
        }
    }
```

We can also make use of a built-in sorting algorithm. Arrays can be sorted into their natural order using the **sort** method of the Arrays class.

```
int[] numbers = {8, 3, 7, 9, 1, 2, 4};
Arrays.sort(numbers);
System.out.println(Arrays.toString(numbers));

// [1, 2, 3, 4, 7, 8, 9]
```

Lists can be sorted into their natural order using the **sort** method of the Collections class.

```
ArrayList<Integer> numbers = new ArrayList<>();
numbers.add(8);
numbers.add(3);
numbers.add(7);
Collections.sort(numbers);
System.out.println(numbers);

// [3, 7, 8]
```

### Linear Searching

In linear search algorithm, the array is checked one index at a time starting from 0. The sample program searches the list for a book with an id variable that matches the value of searchedId parameter it received.

```
    public static int linearSearch(ArrayList<Book> books, int searchedId) {
        for (Book currentBook : books) {
            if (currentBook.getId() == searchedId) {
                return books.indexOf(currentBook);
            }
        }
        //not found
        return -1;
    }
```

### Binary Searching

It is also called logarithmic search. The data should be arranged in order.

```
    public static int binarySearch(ArrayList<Book> books, long searchedId) {
//PSEUDO CODE
//begin = 0 // the 0th index of the list (i.e, the first index of the list)
//end = size(list) - 1 // the last index in the list
//
//repeat until begin is larger than end:
//    middle = (end + begin) / 2
//
//    if the value at list[middle] is searched
//        return the value of the variable middle
//
//    if the value at list[middle] is smaller than searched
//        begin = middle + 1
//
//    if the value at list[middle] is larger than searched
//        end = middle - 1
//
//return value -1

        ArrayList<Book> bookList = books;
        //index range initialize
        int startpoint = 0;
        int endpoint = books.size() - 1;

        while (startpoint <= endpoint) {
            int midpoint = (startpoint + endpoint) / 2;
            
            //found
            if (searchedId == books.get(midpoint).getId()) {
                return books.indexOf(books.get(midpoint));
            }
            if (searchedId > books.get(midpoint).getId()) {
                startpoint = midpoint + 1;
                continue;
            }
            if (searchedId < books.get(midpoint).getId()) {
                endpoint = midpoint - 1;
                continue;
            }
        }
        //fail when start < end
        return -1;
    }
```

