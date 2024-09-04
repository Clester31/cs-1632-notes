# Lecture 3 - Test Plans and TM

## Test Plans

### What is a test plan

* **Test Plan**: A document laying out a plan for testing a software system
  * Needed for minimizing risks of defects given a time/cost budget
  * Careful planning is needed to maximize test coverage
 
* Why do we need to document the plan?
  *  So project managers to estimate test coverage and manage risk
  *  So QA engineers can repeat the same tests over and over (repeatability is important for regression tests)

### Regression Tetst

* **Regression**: failure of a previously working feature
  * Can be caused by unrelated enhancements or defect fixes
  * Regression tests are run on each code update
 
* Regression tests are useful for pinpointing defective versions
  * In the example below, we can see that version 34 is where the defect occurs 

![image](https://github.com/user-attachments/assets/c305e424-1482-41e2-b5bc-b7e554067841)

## Test Cases

### Test Plans and Test Cases

* A test plan consists of a list of related test cases that are run together
* _Test case_: a test sceario with precise steps on how to preform it

### Test Case Main Body

* Preconditions: State of system before execution steps
  * pacakges X and Y are installed on the system
  * Config gile X contains entry Y
  * Database has table X set up populated with Y entry
 
* Execution Steps: Steps to preform test

* Postconditions: **Expected** state after execution steps
  * Derived from requirements based on preconditions + execution steps
 
### Test Case Header

* _Identifier_: A way to identify the test case
  * Could be numerical (TC-452) or descriptive (INVALID-PASSWORD-THREE-TIMES-TEST)
 
* _Tets Case_: a short description of what is being tested

#### A test case contains the following items:

* Identifier
* Test Case
* Preconditions
* Execution Steps
* Postconditions

### Test Run

* **Test Run**: Actual execution of a test case
  * Subsets of test cases may be chosen to run from the entire test suite
  * All depends on the type of code modification and the testing context
 
* The purpose of a test run is to obtain observed behavior
  * passes or fails after comparing observed behavior with postcondition
 
#### Test Run Statuses

* PASSED: Completed with expected result
* FAILED: Completed but unexpected result
* PAUSED: Test paused in middle of execution
* RUNNING: Test in the middle of execution
* BLOCKED: Did not complete because precondition not fulfilled
* ERROR: Problem with running test itself

* During a test run, tester will manually/automatically execute each test case and set the status for each

## Creating Good Test Cases

### A good test case is two things

* Verifies requirements faithfully
  * No false positives or false negatives
 
* Is Repeatable
  * Consistend of who/when/where the tests are run
 
### Pitfall 1: Using observed behavior for Postcondition

* Never use screenshots (or copy/pasted) output even if correct - could cause false positives
* Postconditions should be derived from requirements

### Pitfall 2: Using requirement for postcondition

* Never paste requirements verbatim as postconditions
  * Forces tester to derive expected behavior based on own interpretation
  * Results in unrepeatable tests and false negative/positive defects
 
### Pitfall 3: Imprecise Preconditions / Execution Steps

* Incomplete preconditions (OS/DB/Filesystem/Memory State)
  * ex: OS environment variable that impacts test case is not specified
 
### Sweet Spot

* Documenting preconditions as preconditions
  * If conditions are already satisfied, no need to perform - saves time (no need to install an OS if already installed)
  * Does not enforce same steps to reach condition - less repeatable (OS may have been installed with different options)
 
* Documenting preconditions as initial execution steps
  * Enforces same steps resulting in a more uniform condition - more repeatable (installing OS from scratch resutls in a more uniform environment)
  * Sometimes preformed even when redundant - wastes time
 
### Pitfall 4 - A test case that is not independent

* Test cases shuold not depend on the execution of a previous test case
* Results in an unrepeatable test case

### Pitfall 5 - A test case testing multiple scenarios

* Test cases should not merge multiple scenarios into one
  * On fail, cannot tell easily which scenario resulted in test failure
  * Ex: Call sqrt(4), then call sqrt(9), then call sqrt(16)
 
## Testing Heirarchy

* A group of test plans make up a test suite

![image](https://github.com/user-attachments/assets/0370e015-f9d4-4fef-9dcf-8d3ea613313e)

### Creating a test suite from requirements

* Take a top-down approach to create heirarchy of test plans and cases.

* 1. Subdivide System into features or subsystems
  2. For Each feature, create a test plan with varied inputs + preconditions
  3. For each input + precondition, create a test case
 
* Tets base/edge/corner cases for each feature to maximize coverage

## Traceability Matrix

### TGraceability

* Forward Traceability
  * Ability to trace requirement -> test case
  * Given a requirement, allows listing of all test cases that test it
  * Ensures there are no requirements with insufficient test coverage
 
* Backwards Traceability
  * Ability to trace test case -> requirements
  * Given a test case, allows listing of all requirements that are tested
  * Ensures there are no test cases that are not testing any requirements
 
* Ensures requirements, and only requirements, are implemented 

### Traceability Matrix ensures traceability

* Traceability Matrix: Table describing relationship between requirements and test cases
* Why a matrix?
  * One test case may test multiple requirements
  * One requirement may be tested by multiple test cases
  * Many-to-many relationship 
