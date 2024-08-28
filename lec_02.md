# Lecture 2 (08-28-24)

## Equivalence Classes

### Defining Test Coverage

* Goal of testing: achieve good test coverage
  * **Test Coverage**: Measure of how well the code has been tested
  * Ideally, test_coverage = defects_found / total defects
 
* But is there a way to measure total_defects
  * If we knew, we wouldn't need to do any testing
  * Impossible to measure true test coverage
 
* Proxy to estimate true test coverage
  * **Statememnt coverage** = statements_tested / total_statements
  * Rationale: If a high % of statements are tested, its likely that a high % of defects are found
  * Other proxies: method coverage, path coverage
 
### Improving Test Coverage

* QA engineers have a limited testing time budget
  * Must choose tests maximizing coverage
 
* Which tests are lkely to maximize coverage
  * Tests that exercise *required* program behaviors
  * If tests focus on a subset of program behaviors
    * Cannot find defects in behaviors that are not covered
  * This is the idea behind *equivalence class partitioning*
 
* Observed behaviors are only a subset of the required behaviors
  * If you only check the observed behaviors, you aren't getting the full picture
 
### Equivalence Class Partitioning

* Partition the input values into "equivalence classes"
  * Equivalence class = group of values with the same behavior
 
#### Equivalence classes should be strictly partitioned

* Strictly: each value belongs to one and only one class
* If an input value belongs to multiple classes
  * Means requirements specify two behaviors for the input
  * Either requirements are inconsistent, or were misunderstood
 
### Values can also be objects

* Input values can be tuna cans

* Equivalence classes: ```{not_expired, expired_and_not_smelly, expired_and_smelly}```

* Behavior for each equivalence class
  * Not expired: eat
  * expired and not smelly: feed it to your cat
  * expired and smelly: discard
 
### Testing each equivalence class 

* Pick at least one value form each equiavlence class
  * Ensures you cover all behavior expected from program
  * Good coverage without exhaustive testing 

### Defects are prevalent at boundaries

* Emperical truth: **Defects are more prevalent at boundaries of eqivalence classes than in the middle**
* Why? Due to prevalence by off-by-one errors

### Equivalence class partitioning
    
![image](https://github.com/user-attachments/assets/3efbd21c-2e70-487c-9c7b-fed88800b124)

Boundary values: 34 and 35
Interior values: 26, 30, 39, 42

### implicit (hidden) boundary values

* Explicit boundaries: Specified in requirements
  * Boudnaries that are defined by equivalence classes
* Implicit boundaries: not in requirements
  * "naturally" occurring boundaries in language, hardware, domain
  * Language boundaries: MAXINT, MININT
  * Hardware boundaries: memory space, hard drive space
  * Domain boundaries: weight >= 0, 0 <= score <= 100, etc
 
### Implicit boundaries should not change behavior

* Why do we check explicit boundaries?
  * to verify behavior changes when boundary is croseed
* Why do we check implicit boundaries?
  * To verify behavor does not change on the boundary
 
#### Add implicit boundary values

![image](https://github.com/user-attachments/assets/8972cad2-add8-41cc-9bd3-a1cab5ee0f42)

* Language boundaries: MININT, MAXINT
* Domain boudary: age >= 0 (age is typically non-negative)

### Best, Edge, and Corner cases

* Base case: A typical use case
  * Interior value of equivalence class for normal operation
* Edge case: A use case at the limit of allowed use
  * Boundary value of equivalence class for normal operation
* Corner case (or pathological case):
  * Multiple edge cases happening simultaneously
  * Or value far outside normal operating parameters
 
#### Example

* Suppose a cat scale has these operating envelopes:
  * Weight between 0-100 lbs
  * Temperature between 0-120 F
* Base cases: (10 lbs, 60 F), (20 lbs, 70 F)
* Edge ases: (100 lbs, 70 F), (10 lbs, 0 F)
* Corner case: (10000 lbs, 70F), (100 lbs, 120 F)
  * Why test 10000 lbs?
    * Even if the scale is not expected to correctly operate, the user should still know what happense
   
![image](https://github.com/user-attachments/assets/8a0f986f-e65d-44bd-8a1d-aad52c0d7d8a)

## Categorires of testing (Black, White, Gray, Dynamic, Static)

### Black, white, and gray box testing

* **Black box testing**
  * Testing with no knowledge of interior structure source code
  * Tests are preformed from the user's perspective
  * Can be preformed by lay people who don't know how to program
  * Examples:
    * Tests are preformed only using UI 
 
* **White box testing**
  * Testing with explicit knowledge of the interior structure and codebase
  * Tests are preformed from the developer's perspective
  * Examples:
    * Tests sre preforemd using both UI and explicitly calling methods
 
* **Gray box testing**
  * Testing with some knowledge of the interior structure and codebase
 
### Static vs Dynamic Testing

* Dynamic testing = code is executed
  * Reslies on good inputs for coverage
 
* Static testing = code is not executed
  * There are no inputs since code is not executed (ex: compilation)
  * Relies on analyzing the code to find defects

#### Dynamic testing

* Code is executed under various test scenarios
  * varying input values, compilers, OSes, etc
  * Observed results are compared with expected results
  * Hard to achieve 100% test coverage
 
#### Static testing

* Code is analyzed by a person or testing tool
  * While checking whether correctness rules are followed
  * 100% of test coverage achieved by person checking.


## Requirements and Requirements validation

### What are requirements

* Specifications of software that define expected behavior
   * Often collected into an SRS, *Software requirements specification*
   * The SRS comes in legal binders hundereds of pages long
   * The SRS is often legally binding
 
### Requirements evolve

* Requirements are not set in stone and do evlolve
* Requirements engineering: managing and documenting requirements

### Requirements validation

* Reuirements validation: Are we building the **right software?**
* Requirements verification: Are we building the **software right? (testing)**

#### Aspects of reuqirements validation

* Is the SRS internally sound?
  * Check for consistency, ambiguity, and completeness
 
* Does the SRS satisfy needs and constraints?
  * Check for validity, realism, and verifiability
 
### Pitfall: specifying HOW, not WHAT

* Users care about what the software does, not "what" the user has in mind
  * Specifying "how" may not acieve the "what" user has in mind
  * SPecifying how restricts developers from improving implementation
  * Specifying how often fails the verifyability test
    * Often source code is not available to end user to verify the "how"
   
![image](https://github.com/user-attachments/assets/1460afbd-82dc-44f4-8ccd-b0546c7a57a9)


## Fuctional requirements and non-functional requirements

### Functinoal requiurements

* Specify functional behavior of system
* The system shall do X on input Y

### Non-functional requirements

* Specify overall qualities of system, not a specific behavior
* The system shall be X during operation
  
