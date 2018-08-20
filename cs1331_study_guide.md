# Java Itself
Good Things: cross-platform deployability and automatic garbage collection (no memory management issues)

### Platform Components
1. Java programming language - to write `.java` source files
2. JVM (Java Virtual Machine) - runs compiled source files (`.class` bytecode files, which can be run on any machine with the JVM)
3. Java standard library

### `public static void main (String[] args)`
A main method must be included for a class to be executeable.

---
# Input/Output
### `System.out.printf`
Basically the way you print things in `C`.

`System.out.printf("%d %s.\n", 7, "Samurai");` prints `7 Samurai.`  
`System.out.printf("I like %3.2f.%n", Math.PI);` prints `I like 3.14.`

### Scanner (`java.util.Scanner`)
To read input from the console.
```java
Scanner keyboard = new Scanner(System.in);
System.out.println("Enter your 3 test scores, separated by spaces.");
exam1 = keyboard.nextInt();
exam2 = keyboard.nextInt();
exam3 = keyboard.nextInt();
examAvg = (exam1 + exam2 + exam3) / 3.0;
System.out.printf("Your exam average is %.1f%n", examAvg);
```

You can do this with a file too.
```java
Scanner fileScanner = new Scanner(new File("ScannerFun.java"));
while (fileScanner.hasNext()) {
    String line = fileScanner.nextLine();
    // do something with line
}
```

### File Output with `PrintStream`
`System.out` uses the `stdout` file descriptor.  
You can redirect this to wrtie to files.
```java
PrintStream outFile = new PrintStream(new File("somefile.txt"));
outFile.println(...);
```
---
# Control Structures
### `switch`
Don't use it.

### `for` loop
```java
for(initializer; condition; update) {
    // executes as long as condition is true
}
```
Declare loop indices within for, rather than intializing a variable outside like in `C`.

You can have multiple loop indices.
```java
String mystery = "mnerigpaba", solved = "";
int len = mystery.length();
for (int i = 0, j = len-1; i < len/2; i++, j--) {
    solved += mystery.charAt(i) + mystery.charAt(j);
}
```

---
# Classes
### Abstraction
Capturing the essential properties and behaviors of a concept by ignoring irrelevant details.
- **Process abstraction:** group the operations of a process in a subprogram and expose only essential elements to clients through subprogram signature (e.g. function name and parameters)
- **Data abstraction:** encapsulation of data with defined operations

### ADT
An ADT is *abstract* because the data and operations of the ADT are defined independently of how they are implemented. It *encapsulates* the data and operations.

### Java
Provides language support for defining ADTs - classes.  
A class is a blueprint for objects, and contains:
- **instance variables:** the state of data of an object
- **methods:** operations defined on objects of the class

Objects are *instantiated* or *constructed* from a class. 

#### For Example:
```java
public class Complex {
    // data
    private double real;
    private double imaginary;
    
    // operations
    public Complex(double aReal, double anImaginary) {
        real = aReal;
        imaginary = anImaginary;
    }
    
    public Complex plus (Complex other) {
        double resultReal = this.real + other.real;
        double resultImaginary = this.imaginary + other.imaginary;
        return new Complex(resultReal, resultImaginary);
    }
}
```

### Reference Variable
These have one of two values:
- the address of an object in memory (e.g. and instance of Complex)
- `null`, which references nothing

```java
Complex a = new Complex(1.0, 2.0);
Complex b = new Complex(3.0, 4.0);
Complex c = a.plus(b);
```
`a`, `b`, and `c` are reference variables of type `Complex`. 

### Constructors
Calling `new` invokes the constructor, instantiating an object and storing in a given variable. 
```java
Complex a = new Complex(1.0, 2.0);
```
Looks something like this:
```
 ___         _________________
|_a_| ----> |_____Complex_____|
            | real = 1.0      |
            |_imaginary = 2.0_|
```

### Classes
With the `Complex` class, users can write code to manipulate `Complex` objects using only the public methods of the class.

A class file contains:
- import statements
- class declaration
- static variable definitions
- instance variable definitions
- constructors
- public methods
- private helper methods

### Class Invariants
A condition that must hold for all instances of a class in order for them to be considered valid.

Invariants for the `Card` class:
- `rank` must be one of `{"2", "3", "4", "5", "6", "7", "8", "9", "10", "jack", "queen", "king", "ace}`
- `suit` must be one of `{"diamonds", "clubs", "hearts", "spades"}`

```java
public class Card {
    private String rank;
    private String suit;
    
    public Card(String rank, String suit) {
        setRank(rank);
        setSuit(suit);
    }
    
    private final String[] VALID_RANKS = 
        {"2", "3", "4", "5", "6", "7", "8", "9", "10", 
         "jack", "queen", "king", "ace};
    
    private void setRank(String rank) {
        if (!isValidRank(rank)) {
            System.out.println(rank + " is not a valid rank.");
            System.exit(0);
        }
        this.rank = rank;
    }
    private boolean isValidRank(String someRank) {
        return contains(VALID_RANKS, someRank);
    }
    private boolean contains(String[] array, String item) {
        for (String element: array) {
            if (element.equals(item)) return true;
        }
        return false;
    }
    // ...
}
```

### Static Members
These are shared with all instances of a class.
```java
public static final String[] VALID_RANKS = 
    {"2", "3", "4", "5", "6", "7", "8", "9", "10", 
     "jack", "queen", "king", "ace};
public static final String[] VALID_SUITS = 
    {"diamonds", "clubs", "hearts", "spades"};
```
Each instance shares a single copy of VALID_RANKS and VALID_SUITS. Since they're `final`, they can be safely made `public` so clients can use them.

---
# Arrays
- dynamically allocated
- fixed type and number of elements
- objects, so variables can be `null`

### Declaration
```
double[] scores = new double[5];
```
- `scores` stores the address of the new array
- each value is initialized to the default for its type (`0`, `false`, `null` for references)

Some Ways to Declare
|---|
`double[] scores`
`double scores[]` (do the first one though)
`double scores[], average` (a mixed declaration)

A Way to Initialize
|---|
`String[] validSuits = {"diamonds", "clubs", "hearts", "spades"};`

### The Enhanced `for` Loop
Use when you don't need the index.
```
// for each element of the array
for (type element: array) {
    ...
}
```

For example:
```java
double sum = 0.0;
for (int i = 0; i < scores.length; i++) {
    sum += scores[i];
}
```
can be turned into:
```java
double sum = 0.0;
for (double score: scores) {
    sum += scores;
}
```

### Run-time Errors
- `double[] scores = new double[-5];` compiles because arrays are allocated dynamically
- `scores[-1] = 100;` same with access expressions (ArrayIndexOutOfBounds)

### Parameters
*arity* is the number of formal parameters in a method.  
The last parameter may be a *variable arity parameter*, which is accessed as an array inside the method.
```
public static int max(int ... numbers) {
    int max = numbers[0];
    for (int i = 1 ; i < numbers.length; i++) {
        if (numbers[i] > max) max = number;
    }
    return max;
}
```
