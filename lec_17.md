# Lexture 17

## Symbolic Model Cecking

* Model checking can be categorized into:
  1. eunmerative model checking
    *  What we learned last chapter
    *  Hard to escape state explosion   
  2. symbolic model checking
    * What we will learn
    * Model checking using symbolic expressions
 
### Symbolic Execution

* Symbolic execution: Assigning symbolic expressions instead of actual values to variables during execution
  * Instead of x = 1, y = true...
  * x = A + 1, y = A * b
* Symbolic expression: An expression using symbolic values
* Symbolic value: Math symbol that stands for an input value
* Idea: x == A + 1, y == A + 2 at source line assert(x < y)
  * Model checker can prove through math that it always passes, for every input value without having to try them one by one
 
#### Notation

* Program variables are in lower case while symbolic values are in uppercase

### Symbolic Modeling Checking Uses

* Prove a program correct
  * Much less state explosion than enumerative checking
* Generate test vectors that exercise each path
  * For the purposes of increasing test coverage of code
  * The output sets of the constraint solver are the test versions
* Generate Program invariants
  * Invariants enhance programmer's understanding of code
  * The path conditions themselves are the invariants
 
### Best of Both Worlds

* Concolic = Concrete + Symbolic
