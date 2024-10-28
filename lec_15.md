# Lecture 15 - Static Analysis Part 1

## Intro

### Dynamic vs Static Testing

* Dynamic test - code is executed by the test
* Static test - Code is not exectued by the test
  * defect found through analysis of code
 
### Why Static Test?

* Often easier than dynamic testing
  * No need to come up with test cases
  * No need to set up software or run the program
 
* Can pinpoint a defect better than a dynamic test
  * Static test analyzes the code and tells you exactly what to fix
 
* Can often find defects missed by dynamic testing

### Why not (only) static test

* Does not find all defects
* Often reports false positives (defect reported when there isn't one)

## Compiling

### Compiler

* First job of compiler is to translate source code to machine code
* Second job is to perform static checks on source code
  * Error - code does not adhere to language rules (syntax, type)
  * Warning - code adheres to language rules but looks suspicious
 
* Warnings are their weight in gold
  * Programmers tend to fix errors but ignore warnings since it still compiles
 
* Let your compiler do static checking to the fullest

### Choice of language is important

* Language decides effectiveness of compiler static analysis
  * The more semantic information is exzposed, the more effective the analysis 
* Language features that help / harm compiler check
  * Strong data types in Java
  * Weak data types in JavaScript
 
## Code Coverage

* How much of the codebase is covered by a particular test suite
* You need to execute a test suite so isn't this dynamic testing?
  * Yes, but a fiar bit of static analysis is required to measure code coverage
 
* Code coverage can mean different things though

### Method Coverage

* Number of methods in the class covered by tests / total methods in the class

![image](https://github.com/user-attachments/assets/de7423c7-3eb9-47d9-8fa7-55a4ad328522)

### Statement Coverage

* Number of statements in method covered by tests / total statements in the method

![image](https://github.com/user-attachments/assets/89ea44f1-331f-49fd-ae8a-f4769d59fd6c)

### Other kinds of Code Coverage

* Branch Coverage: % of branch directions (if statement) covered
* Condition coverage: % of boolean expressions covered
* Path coverage: % of paths in methods covered
* Parameter value coverage: % of (common) parameter values covered
* Entry/Exit coverage: % of method calls / returns covered

* Remember, all are proxy metrics for the ideal coverage metric

### What does statement coverage tell us?

* Where more tests would be userful and where tests are missing
* 100% code coverage does not mean defect free

#### What statement coverage can't catch

* Defects triggered by different input values that cover the same paths
* Defects on a path with covered statements but was never traveresd

## Linters

* Poorly written code can cause issues
* Multiple people writing code in different styles can cause issues

### Linters enable a team to use the same style

* Used very commonly, because its easy to use
* Any SW company has a style guide
* Style guide can be documented and passed to the linter

### Linters

* Standalone
  * CheckStyle: Java Linter
  * CppLint: C++ Linter
  * ESLint: Javascript Linter
 
## Bug Finders

* Looks for patterns that are common signs of defects
  * False positives: pattern match not necessarily a defect
  * False negatives: bug that doesn't fit pattern won't get detected
 
* Pattern match may signal
  * Defect
  * Confusing code
  * Performance issues
  * Security vulnerabilities
 
### Bug Finder Tools

* Java
  * Findbugs: bug-finder static analysis software
  * Spotbugs: A successor to Findbugs
 
* C/C++
  * CppCheck: Findbugs equivalent for C/C++
  * Splint: Bug finder with focus on security vulnerabilities  
