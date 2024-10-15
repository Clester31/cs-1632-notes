# Lecture 13 (10-15-24)

## What is testing so far

1. Split the set of input values into equivalence classes
2. choose a few representative values from each equivalence class
3. Write test case for those few values

* Imagine an entire suite of test cases...
  * At what point would we be satisfied?
    * There is a near infinite number of sequences we could test
    * Each sequence is a unique equivalence class
    * Each execution path represents a unique behavior
  * Verdict: It is impossible to write enough tests to cover all behavior
  * But could we auto generate them?
 
## Stochastic Testing

* Stochastic testing: testing using randomly generated input values
  * Although we still are not testing all inut values, we're just testing a large number of random values hoping for good coverage
 
* Also called "Monkey Testing"
  * Testers should give *a lot* of thought into how input values are generated
  * Testers should choose a distribution most likely to uncover defects
 
### Good distribution of Values is important  

```java
void foo (int x, int y) {
 if (x == y) {
 // Defect occurs
 }
}
```

* If we blindly test random combinations of x and y, there is a low probability where x == y is chosen
* And a low probability that the defect is found with randomization
* A good distribution contains cases where x == y

### The Test Oracle Problem

* So now we have a set of randomly generated input values
* How do we auto generate expected output values?
  * We need an oracle to tell us what the expected outcome should be, otherwise, output values must be calculated by humans one by one
 
* **What if we tested properties instead of output values?**

## Property Based Testing

* *Property Based Testing*: Testing correctness properties of observed values
  * Property: something that invariably holds true in observed values
  * properties are also called invariants
  * Does not test "observed == expected"
  * No need to generate expected values are part of the test
 
* **Properties allow testing of any random input values**

### Invariant examples

* a = b + c
  * assuming b > 0 and c > 0, a > 0 always holds true
  * assuming b < 0 and c < 0, a < 0 always holds true
* a = b - c
  * assuming b > c, a > 0 always holds true
  * assuming b < c, a < 0 always holds true
 
* Property based testing does not guarantee correctness
  * But if you check enough properties you often get pretty close
 
### Pros and Cons -> Property based testing

* Disadvantages
  * Does not always guarantee that each output value will be correct 
* Advantages
  * Can check behavior without being provided expected output values
    * Enables stochastic testing
    * Can be embedded in source code to check values at runtime
  * Good for thinking about invariants and improve code
 
### Pros and Cons -> Stochastic Testing

* Advantages
  * Can achieve high test coverage with minimum effort
  * Test input values not biased by preconceptions tester has about code
  * Coders get to understand invariants in code, which leads to code improvement
* Disadvantages
  * Due to property testing, does not always guarantee output value correctness
  * Tests are **not repeatable**
 
### Sotchastic Testing and Repeatability

* Reproducability vs Repeatability
  * Reproducability: Ability to reporduce a defect found by a test
  * Repeatability: Ability of a test to repeat itself every time it is run
 
* Stochastic tests are reproducible
  * Tester only needs to record randomly generate input value causing defect
  * Tester can pass on input value to coder to reproduce the efect
 
* Stochastic tests are not repeatable
  * Every time the test runs, a new input value is tested by design
  * Even when defect is present, test may pass or fail depending on time of day
  * Very hard to figure out when defect was introduced
 
#### Best practices for Stochastic tests   

* Stochastic testing should not be a main method of testing
* Use repeatable tests to the fulest (concrete values)
* Use Stochastic testing as a second line of defense

### QuickCheck

* Two simple steps
  1. Specify the properties of the allowed input
  2. Specify the properties of the output that must hold (invariants)
 
* Example

```java
@Property public void testConcat(String s1, String s2) {
 assertEquals(s1.length() + s2.length(),
 (s1 + s2).length());
}
@Property public void testSqrt(@InRange(minInt=0) int n)
{
 if(n > 1) assertTrue(n > sqrt(n));
}
```

* @Property: 100 randomized trials are done on the property-based test
* @InRange: constraints the range of randomized input values

### Shrinking

* Finds the smallest possible input that triggers a failure
* Helps track down actual issue
* A "toy" failure is a great thing to add to a defect report

## Fuzz Testing

* A form of stochastic testing with a focus on "byte stream" inputs
* Idea: feed a program with "fuzzy" or "noisy" byte streams and see if it
  * Exposes a defect (most commonly a system crash)
  * Exposes a security vulnerability
 
* A byte stream can be as varied as...
  * Input file to a image viewer or video player
  * A network packet to a web server
  * Javascript code interpreted by a web browser
  * A configuration file for a program
 
### Smart Algorithm for Fuzz Testing

* New test plan for web browser
  * Start from a collection of existing HTML files (corpus)
  * "Fuzz" HTML files in corpus to create new variants and add to corpus
 
* Steps to "fuzz" HTML files
  * Parse an HTML file
  * Mutate parts of parse tree with new values
  * Regenerate HTML file from parse tree and test on web browser
  * Only add to corpus if the new HTML file increases code coverage
  * Stop if sufficient code coverage is achieved, otherwise loop back to 1  
