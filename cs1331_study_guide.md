# Java Itself
Good Things: cross-platform deployability and automatic garbage collection (no memory management issues)

### Platform Components
1. Java programming language - to write `.java` source files
2. JVM (Java Virtual Machine) - runs compiled source files (`.class` bytecode files, which can be run on any machine with the JVM)
3. Java standard library

### `public static void main (String[] args)`
A main method must be included for a class to be executeable.

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
