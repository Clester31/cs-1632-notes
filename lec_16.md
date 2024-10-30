# Lecture 16 - 10-30-24

## Model Checking

### Formal Verification

* Proving one or the other about a program
  * Program has no defect
  * Program has defects (and find all of them)
 
### Methods of Formal Verification

* Theorem Proving
  * Deducing postcondition from precondition through math
 
* Model Checking
  * Given a finite state model of a system, exhaustively checking all the states to see if model meets a given specification
 
### Hoare Logic Theorem Proving

* Hoare Logic: Proves a Hoare Triplet through mathematical deduction
* Hoare Triplet: {Percondition} program {Postcondition}
  * Meaning: Given Precondition and Program, Postcondition is always true
 
* Hoare Triplet Examples
  * { True } x = A { x == A}
  * { True } x = 5; x = x + 3 { x == -2}
 
### Theorem Proving Advantages

* Can prove large programs with many (infniite) states
  * Model checker needs to visit each state to verift property is true
  * Prove { True } if (x < 0) then x = -x { x >= 0 }
 
* Leads programmer to deeper understanding of the system

### Theorem Proving Disadvantages

* Requires a lot of human involvmenet
  * Automated theorem provers often need human assistance
  * Highly skilled people with formal methods training is needed
 
* Automated proofs can be obscenely long
  * Hard for humans to comprehend and double check the proof
 
### The Model Checking Problem

* Does implementation satisfy specifications
* Implementation is also called a system model
  * System model can be just your source code
  * Or some abstract model derived from source code
 
* Specification is also called a system property
  * The same "property" in proerty based testing
 
### Example of system properties

* Memory related properties
* Thread related properties
* User assertion properties4

### State Explosion

* Non trivial programs have many more states in their FSMs
  * May run into memory/itme limitations
  * This iscalled **State Explosion Problem**
 
* Single reason preventing wide adaptation of model checking
* State matching & backtracking alleviates this problem but not all of it

### State exploration with Matching & Backtracking

* State divergence happens when there is a choice
  * Value from random number generation or user input
  * Choice of thread to run amoung multiple threads
* Match
  * When next state matches a previously visited state
  * Backtrack to not repeat work
* Backtrack
  * On reaching terminal state or when there is a match
  * Go to closest previous state with unexplored transition     

### State Space Explosion is sometimes unavoidable

* Even with state matching, sometimes state space explodes

* May have to filter our part of program state that causee explosion
  * Human has to tag variables or objects as filtered
  * May result in parts of program state that are not verified 
