# Lecture 12 (10/07/24)

## Key Idea's

* Segment code - make it modular
* Don't Repeat Yourself
* Move TUFs out of TUCs
* Make it easy to satisfy preconditions
* Make it wasy to reproduce
* Make it easy to localize

### Segment Code

* Methods should perform one well-defined functionality
  * BAD: setDatabaseAndGetNumMonkeys()
  * GOOD: setDatabase(), getNumMonkeys()
  * More modular and removes dependability while testing
 
### Don't Repeat Yourself

* Don't copy and paste code
* Dont have multiple methods with the same functionality

* Leads not only to a bloated codebase
  * Twice the amount of code to maintain
  * Twice the room for error
 
* Leads to less testable code
  * Twice the amount of testing you need to do
  * When a defect is found, bug fix must be replicated in all copies of code
 
#### How do you not repeat yourself?

* For duplicate code, create a new method and call that instead
* For two (or more) similar methods, merge them into one
* What happens if two codes are functionally similar only with different types?
  * Use polymorphism (subclassing, subtyping, inheritance)
  * Use a variable that can take on different types at runtime
 
* Make use of generic classes and methods
  * Classes and methods that have paramaterized types
 
### Move TUFs out of TUCs

* No Test-Unfriendly Features (TUFs) inside of Test-Unfriendly Constructs (TUFs)
* Do not put code that you want to fake (TUFs) inside methods that are hard to fake (TUCs)

#### Test Unfriendly Features (TUFs)

* Feature that you typically want to fake useing stubs
  * Features that take too long to set up to work correctly
  * Feature takes too long to test (I/O)
  * Testing feature can cause unwanted side effects
 
* Examples:
  * Printing to console
  * reading/writing from a database or filesystem
  * Accessing a different program or system
  * Accessing the network
 
#### Test Unfriendly Constructs (TUCs)

* Methods that are hard to fake using stubbing or overriding
  * Stubbing: replacing a method in a mocked object using Mockito
  * Overriding: overriding a method in a "fake" class that subclasses real class
 
* Examples:
  * Object constructors / destructions: impossible to override
  * Private/Final methods: impossible to override
  * Static methods: impossible to override/stub

### Make it easy to satisfy conditions

* Dependence on external data == bad for testing
* External data:
  * global variables
  * Values extracted from a global data structure
  * value read from a file or database
  * value that is not passed in as an argument
  * AKA side effects   

```java
// Bad
public float getCatWeight(Cat cat) {
  int fishWeight = Fish.weight;
  // Because the cat ate the fish
  return cat.weight + fishWeight;
}
```

* Bad because Fish.weight is external data not in arguments

```java
// Better
public float getCatWeight(Cat cat, int fishWeight) {
  return cat.weight + fishWeight;
}
```

* If we have to access external data somewhere, where do we do it?
  * If you pass data using arguments, you will need less external data
* For the remaining external data
  * Segregate hard to test code with side effects into a small corner
  * Keep as many methods *pure* as possible
 
### Make it easy to reproduce

* Dependence on random data == bad for testing
  * Random data makes it impossible to reproduce result
 
```java
// Bad
public Result playOverUnder() {
  // random throw of the dice
  int dieRoll = (new Die()).roll();
  if (dieRoll > 3) {
    return RESULT_OVER;
  }
  else {
    return RESULT_UNDER;
  }
}
```
```java
public Result playOverUnder(Die d) {
  int dieRoll = d.roll();
  if (dieRoll > 3) {
    return RESULT_OVER;
  }
  else {
    return RESULT_UNDER;
  }
}
```

* Why Better? Now we can mock Die and stub d.roll();
* 
```java
Die d = Mockito.mock(Die.class);
Mockito.when(d.roll()).thenReturn(6);
playOverUnder(d);
```
 
### Make it easy to localize

* Also called Dependency Injection
  * Passing a dependent object as argument (rather than building it internally)
    * Makes testing easier by allowing you to mock the object
    * Also what allowed us to mock Die in the above example
    * Has other software engineering benefits like decoupling (easy to switch out of one class for another)
   
## Dealing with Legacy Code

* Legacy code in the real world is often seldom tidy
  * Code is often written hurriedly under pressure, with no consideration for testing
  * Often no documentation and you aren't even sure how the code works

### Pinning Tests

* Pinning test: A test done to pin down existing behavior
  * Note: existing behavior may be different from existing behavior
  * Want to pin down all behvaior, bugs, before modifying
  * Even "defective" behaviors that violate method specs may sometimes be used
    * Make sure that even these don't get accidentally modified
    * If you must modify them without modifying that use case, your software will break!
   
* Pinning tests are typically done using unit testing

### Look for Seams in your legacy code

* Seam in software QA
  * Place where two code modules meet where one can be switched for another without having to modify source code
  * We want to pin down the behavior of each unit in legacy code
  * Seam is a place where fake objects can be injected to localize unit test
 
* Why is it important not to modify the source code?
  * Point of pinning tests is to test the legacy code *as is*
  * If we modify  code, we are in danger of changing behavior

#### Seams in legacy code

* Code with no seams
  
```java
String read(String sql) {
  DatabaseConnection db = new DatabaseConnection();
  return db.executeSql(sql);
}
```

* Hard to unit test since we are forced to work with a real DB connection
  
* Code with seam:

```java
String read(String sql, DatabaseConnection db) {
  return db.executeSql(sql);
}
```

* Easy to unit test by passing a mock db and stubbing db.executeSQL()

### Refactoring Legacy Code

1. Write pinning tests for the classes you will be refactoring (make use of seams)
2. Refactor a method
3. Run pinning tests to make sure existing behavior did not change
4. Repeat steps 2 and 3 for every method you want to refactor
