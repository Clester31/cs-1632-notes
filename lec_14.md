# Lecture 14 - Nondeterminism and QA

## Nondeterminism

* When the output of a problem is not determined by its input
* A deterministic program produces the same output on the same input:

![image](https://github.com/user-attachments/assets/015f5ef2-59c6-45a3-b187-783f4e5a23a2)

* A non-deterministic output produces different outputs on the same input

![image](https://github.com/user-attachments/assets/2b7f73ba-46f2-41ca-962f-a59f4b858b38)

### Nondeterminisn Makes Testing Hard

* Surprise defects
  * Defects not revealed during testing suddenly pops up during usage
 
* Unreproducible defects
  * Defect revealed during testing does not show up when trying to debug it
 
### What to do?

* Depends on what kind of nondeterminism it is

1. Nondeterminism by mistake
  * Coder never intended nondeterminism; nondeterminism iteslf is the defect
  * Stamp out the nondeterminism
   
2. Nondeterminism by design
  * Coder intends nondeterminism
  * Must somehow deal with the nondeterminism

### Why non-determinism by design

* Consider the following non-deterministic program

![image](https://github.com/user-attachments/assets/f5b3d114-0dcd-4f07-9385-3e92d06de32c)

* Both outputs are correct since there is no ordering constraint in a set
* Less constraints mean the program can run faster
* A straightforward loop checking each name is deterministic but slow
* What if we use mapReduce() to speed up the program?

#### MapReduce implementation of Filter Names

* Reducer concatenates in the order of arrival -> non-deterministic
* All non-commutative reducers like concatenation have this property
* For determinism, must contain order of mapping -> slows down programs

### Non-determinism by design (cont.)

1. To make programs go faster through parallel execution
  * Sometimes all outputs are equally correct -> nondeterminism is a problem
  * Sometimes, for optimization problems, some outputs are "better" than others
2. To intentionally introduce randomness (random number generator)
  * Video games - to instroduce random events in the game
  * Cryptography - to make cryptography unpredictable

### It's a mistake! - Stamp out from your code

* Due to erroneous code
  * Memory errors
  * Datarace errors
 
* Runtime behavior of the program is undefined or barely defined
  * called errors becuase they are illegal in language specification
 
* Undefined behavior can hardly be intentional by design
  * These behaviors need to be banished
 
#### Does it matter?

* Pointer addresses are almost never part of program output anyway
  * Unless you are printing them out for debugging purposes anyway
 
* But addresses can leak out to program by mistake
  * Specifically when you have memory errors '
 
## Memory Errors

* Errors that access an illegal memory location are the culprits
  * Buffer overflow: access beyond the bounds of an error
  * Dangling pointer: access to an already freed memory pointed to by pointer
 
* If illegal location contains an address, it can leak out to the output

* Only happens in languages like C/C++ with direct access to memory
  * Does not happen in memory managed languages like Java or Python
  * C/C++ is used to write most system code so it's a big problem 
