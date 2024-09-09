# Lecture 5 (9/9/24) - Unit Testing

## What is unit testing?

* Unit Testing: Testing "small" units of code instead of the whole system
* Goal: Ensure unit works independent of the rest of the system

## Why Unit Test 

* System -> Subsystem -> Modules
* Unit testing can localize the bug into a very small unit

### Unit Testing is usually done by developers

* Unit test code is developed in concert with implementation code
* Developers know bset about the behavior of individual methods
* Allows immediate testing without waiting for other units to complete

## Why Do Unit Testing?

1. To localize defects to a small unit of code
2. Can perform testing early on during development (shift left)
3. Unit tests serve as "living documentation"

## JUnit Framework

* JUnit - A framework for automated unit testing of Java programs
* Composed of annotations + assertions

### JUnit Annotations

* Annotations are used to indicate special methods to JUnit
  * @Test: Method run as a test case when JUnit is invoked
  * @Before: A method that sets up a common set of preconditions before running each test case
  * @After: A method that tears down the test fixture set up by @before
 
* A JUnit test class has multiple @Test methods but only one set of @Before and @After annotations

### JUnit assertions

* Assertions are used to check postconditions

![image](https://github.com/user-attachments/assets/9f50b630-6e87-4f4b-b88e-91a28f2f1930)

* assertSame: asserts that two references refer to the same object
* assertEquals: Asserts that two objects are equal
* fail: always fails. Indicates code location should not be reached

# Unit Testing Part 2

## Unit Testing fake objects for dependencies

* Called Test Doubles. Pretend to be the real thing but isn't
* Goal: To not execute code in external classes as part of the unit test
  * Means if a defect is foudn, it is localized to within the tested method
  * Means method can be tested with dependent classes still under development
 
* Test Double appears like the real thing to tested method
  * Even if double does not execute code in the external class
  * Double emulates the real object's behavior in the given test scenario
 
### Mocking: Creates Fake Object with no code

* ```java
  fake = Mockito.mock(fake.class)
  ```
* Mockito: A framework for creating test doubles
  * Good for emulating test doubles that exhibit simple behavior
  * Uses Java Reflecction + Bytecode REwriting to override method behavior
 
* In Mockito terminology:
  * Test double -> Mock, act of creating a mock -> Mocking

### Stubbing: Allows Mocks to Emulate State

* ```java
  Mockito.when(mock.method()).thenReturn(<value>);
  ```
* What if a precondition specifies a state for a mock objext?
  * E.g. Cat has a name of "tabby" or a net worth of 300 dollars
  * We learned mocks are completely devoid of state or code
  * Manipulate getter methods to return specified state
 
* All objects should have proper data encapsulation:
  * Data Encapsulation is when all member variables are declared private
  * Then only way to query internal state is through getter methods
 
#### Stubbing sets up preconditions

* Fake method -> stub, act of changing method return value -> stubbing

### Behavior Verification: Allows postcondition check on mocks

* ```java
  Mockito.verify(mock).method(arg1, arg2)```
  ```

#### Mock state cannot (and should not) be checked

* What if a post condition specifies a state for a mock object?
  * E.g. cat has a net worth of 300 dollars after being rented out or 3 days
  
* First answer: Cannot be done
  * Mock cat has no state so there is nothing to check
  * What if we emulated the state to check through stubbing
  * ```java
    Mockito.when(cat.toString()).thenReturn("Tabby 300");
    assertEquals("Tabby 300", cat.toString());
    ```
  * This is called a atautological test, because it always passes regardless of defects
 
* Second answer: should not be done
  * You are checking something about Car, which is beyond the scope of testing
 
#### Modifications to Mock state can be checked

* What if the postcondition speifies a modification to the state of a mock object?
  * Cat is given a rent payment of 300 dollars, after being rented out for 3 dats
 
* First answer: can be done
  * Mockito framework keeps track of all calls to mock objects
  * Can check that rent calll has been made (once) with a certain payment argument
  * ```java
       Mockito.verify(cat).rent(payment);
       Mockito.verify(cat, Mockito.times(1)).rent(payment);
    ```
 
* Second answer: Should be done
  * You are checking something about RentACat, that initiates the modification 
