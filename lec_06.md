# Lecture 6 - Test Driven Development

## Hyrum's Law

* "With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody

## TDD

* TDD: A software development methodology where:
  * Tests are written before writing code
  * Write only code that is tested
  * short turnaround cycle
  * Refactoring early and often
 
* It's a development methodology - meant for developers
* THe "test" here means unit test

### Red Green Refactor Loop

* Red: write a test for new functionality
  * Test case should immediately fail (no code has been written yet)
 
* Green: Write only enough code to make the test pass

* Refactor: Review code and make it better
  * Improving code without changing it's functionality
 
### Takeaways of TDD

1. Devlopment is driven by testing
2. 100% test coverage all the time
3. Regression testing all the time
4. Ensures development happens in small incremenets
5. Software quality assurance integrated into development cycle
