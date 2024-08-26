# Lecture 1 (08-26-24)

## Zero-Sum Thinking No Longer Works

* Zero-Sum thinking (Old way)
  * "If you get a larger slice of the pie, I get a samller Slice"
  * If you lose, I win
 
* Everything is connected
  * Pandemic: If my neighbor gets the virus, so will I
 
* Zero Sum thinking no longer works

## Collaboration Beats Competiton

* Before, most software was closed source and proprietery (owned by a single/a few company)
* Today, there is an increasing number of open-source software/products
* Increasing importance of the developer *community*

## Testing Theory and Terminology

### Expected vs. Observed Behavior

* Expected Behavior: What should happen | Observed Behavior: what does happen
* Testing: checking expected == observed
* Defect: expected != observed

* Expected behavior is enforced using **requirements**

#### Example

```Java
// requirement: return square root of a num
float sqrt(int num) { ... }

ret = sqrt(9) // expected behavior -> ret == 3
              // any behavior where ret != 3 is a defect

ret_neg = sqrt(-9) // what is the expected behavior?
                   // maybe we should have some requirement (ex: return 0 for all negative numbers)
                   // Any other observed behavior is a defect
```

### Imposibiity of exhaustive testing

* Testing all combinations of arguments wouldn't exactly guarantee that there are no problems
* Issues not covered by exhaustive input testing
  * Compiler issues
  * System level issues (OS/device dependent defect)
  * Parallel programming issues (race conditions)
 
* The same input also must be tested multiple times

#### Compiler issues

* Compiled binary (not the source code), runs on the computer
* Compilers can (very rarely) have bugs
  * More frequently, compilers can expose a bug in your program
 
* We need to exhaustively verify with all cpmpilers and compiler options
