**Note: the items in bold are learning goals that require application of your
knowledge.  Either you have to apply your knowledge to a piece of code, or you
need to apply a testing tool to a specific problem.**

## TESTING THEORY AND TERMINOLOGY
* **Be able to explain why exhaustive testing is virtually impossible, even with just one method.**
  * Testing each value independently will take an insanely high number of tests, assuming that the boundaries are within MIN_INT and MAX_INT
  * Exhaustive testing also does not guarantee that there will not be any defects   
* **Be able to perform equivalence class partitioning given a set of requirements.**
  * Requirements: In order to be President of the United States, you must be 35 years or older   
  * Classes: {CANT_BE_PRESIDENT, CAN_BE_PRESIDENT}
  * Behaviors
    * CANT_BE_PRESIDENT: Returns "You are not old enough to be president"
    * CAN_BE_PRESIDENT: Returns "You are old enough to be president"
  * Partioning:
    * CANT_BE_PRESIDETNT = {...29, 30, 31, 32, 33, 34}
    * CAN_BE_PRESIDENT = {35, 36, 37, 38, 39, 40, 41...}
      
* **Be able to come up with boundary and interior values given a test scenario.**
  * Boundary:
    * CANT_BE_PRESIDETNT = {...29, 30, 31, 32, 33, **34**}
    * CAN_BE_PRESIDENT = {**35**, 36, 37, 38, 39, 40, 41...}
  * Interior:
    * CANT_BE_PRESIDETNT = {...29, **30**, 31, 32, **33**, 34}
    * CAN_BE_PRESIDENT = {35, 36, 37, **38**, 39, **40**, 41...}
      
* **Be able to differentiate between base, edge, and corner cases.**
  * Base Case: A typical use case, usually an interior value within an equivalence class
  * Edge Case: A use case at the limit of allowed use, usually a boundary value
  * Corner Case: A rare or extreme use case far beyond the standard operating parameters
 
  * ![image](https://github.com/user-attachments/assets/7f66bcd6-d42e-4e5d-b68f-3d75dcd8fa9d)

    
* **Be able to explain the difference between static vs dynamic testing and give examples of each.**
  * Static Testing: Code is **Analyzed** by a person or testing tool
  * Dynamic Testing: Code is **Executed** under testing scenarios
    
* **Be able to explain the difference between black box / white box / gray box testing and give examples of each.**
  * Black Box - Tester has no knowledge of the code base (Game testing, using UI)
  * White Box - Tester has full knowledge of the code base (Passing in parameters to a function, testing exceptions)
  * Gray Box - Tester has some knowledge of the code base (Database testing, Website testing)
    
* **Be able to quantify test coverage**
  * *test_coverage = defects_found / total_defects*
    * Impossible to measure since we can't find a way to find the total number of defects
  * *statement_coverage = statements_tested / total_statements*
    * If a high percentage of statements are tested, its likely that a high percentage of defects are found
   
* **Why are defects more common at boundaries of EQ classes**
  * Off-by-one errors. Take the president EQ class for example. If we set the requirement for being president at > 35 instead of >= 35, then we could have a case where passing in 35 would give us the wrong result.
 
* **Explain Explicit and Implicit Boundary values. Give an example of each**
  * Explicit boundaries: Boundaries that are defined by EQ classes
    * We check these to verify that behavior changes when a boundary is crossed 
  * Implicit boundaries: Boundaries that are not in the requirements but have an impact on the tests
    * MAXINT, MININT, memory space, hard drive space, domain (weight can't be < 0)
    * We test these to verify that behavior does not change on the boundary
   
  * CANT_BE_PRESIDETNT = {**MININT-1**, **MININT**, **-1**, **0**, 1,...,29, 30, 31, 32, 33, 34}
  * CAN_BE_PRESIDENT = {35, 36, 37, 38, 39, 40, 41,...,**MAXINT**, **MAXINT+1**} 

## REQUIREMENTS ANALYSIS
* **Be able to argue why requirements should not specify implementation.**
  * requirements should describe what to achieve, not how to achieve it
  * requirements are almost never set in stone and will change, code must change accordingly
* **Be able to clearly define the difference between requirements verification and requirements validation.**
  * Requirements verification: Are we building the **right software**
    * Do the requirements make sense/are feasable
    * Do they meet the stakeholders needs 
  * Requirements validation: Are we building the **software right** (testing)
    * Derive expected behavior from reqs for each test case
    * Compare expected behavior with observed behavior 
* **Be ready to give a few examples of checks performed during requirements validation and what they mean**
  * validity - does the SRS align with user needs?
  * completeness - does the SRS cover all aspects of the software?
  * consistency - does the SRS contain any logical conflicts?
  * realism - is the SRS something that can be feasibly implemented?
  * ambiguity - does the SRS contain room for interpretation?
  * verifiability - is the SRS something that can be feasibly tested?
 
* **Ostrich Cage Example**
  * The cage shall hosue an ostrich
    * Ambiguity: What kind of ostrich? (baby, audlt)
    * Validity: Do people really want an ostrich in their homes
  * The cage shall be 2 feet tall
    * Consistency: Most ostriches are taller then 2 feet
    * Ambiguity: 2.000 feet or 2.001 feet?
  * The case bars shall be made of candy
    * Ambiguity: What kind of candy?
    * Validity: Candy bars look good but may get eaten
    * Realism: How structurally sound is a cage made out of candy bars? 
  * At least 90% of ostriches must like the cage
    * Verifyability: How can we prove that 90% of all ostriches can like the cage?
    * Ambiguity: How much do they need to like it
  * Completeness:
    * Shape of the cage? width? cage bar thickness? how far apart should the bars be?
   
* **Why is it a bad idea to specify HOW instead of WHAT?**
  * User's care about what the software does, not how it does it
  * May not achieve what the user has in mind
  * Restricts developers from improving implementation
      
* **Be able to differentiate between Functional Requirements vs Non-Functional Requirements (Quality Attributes)**
  * Functional Requirements: specify the functional behavior of the system
    * The system shall **do** X on input Y
  * Non-Functional Requirements: (Quality Attributes): Specify overall qualities of a system, not a specific behavior
    * The system shall **be** X during operation
   
  * Functional Examples:
    * System shall **return** "NONE" if no elements match the query
    * System shall **throw** an exception on illegal parameters
    * System shall **turn on** HIPRESSURE light at 100 PSI
   
  * Non-Functional Examples:
    * System shall **be** protected against unauthorized access
    * System shall **be** easity extensible and maintainable
    * System shall **be** portable to other processor architectures
   
* **Explain the issues with Quality Attributes and how to overcome them**
  * They are difficult to test since they are qualitative, therefore are subjective. They are also difficult to measure
  * Solution: turn qualitative to quantitative
  * Example:
    * BAD: The system shall be highly usable
    * GOOD: Over 90% of users shall be able to operate the software after one hour of training
   
    * BAD: The system shall be reliable enough to be used in a space station
    * GOOD: The system shall have a mean-time-between-failures of 100 years
     
## TEST PLANS
* **Be able to give examples of preconditions and postconditions.**
  * Preconditions: State of the system before execution steps:
    * Packages X and Y are installed on the system
    * Configuration file X contains entry Y
    * Database has table X set up populated with Y entry
  * Postconditions: Expected state after execution steps
    * The system shall display "text"
    * The return value of the function shall be 3        
* **Be able to explain what a regression test is and why it is important.**
  * Regression tests are tests done to test modified features to see if they cause defects in previously working features.
  * Allow developers to pinpoint which update caused a previously working feature to stop working
    
* **Be able to explain what problems in a test case may cause it to become not reproducible.**
  * Pitfall 1: Observed behavior for postcondition
    * Screenshots can contained spurious info that can result in false positive defects
  * Pitfall 2: Using requirements for postcondition
    * Never paste requirements verbatim as postconditions
    * Tester may not be able to tell what the expected return value should be
  * Pitfall 3: Imprecise Preconditions / Execution Steps
    * Incomplete preconditions, such as a missing OS environment variable, can lead to unrepeatable tests
    * Imprecise execution steps too: such as "Open a new browser" -> Multiple ways: Cntr+N, Menu, Double Click
        
* **Be able to explain what problems in a test case cause it to not be independent.**
  * Pitfall 4: A test case that is not independent
    * Tests should not depend on the execution of a previous test case
    * Also results in unrepeatable tests, as if the previous test case fails, the entire test fails
  * Pitfall 5: A test case that merges mutliple scenarios
    * Test cases should not merge multiple scenarios into one
          
* **Be able to explain the hierarchy of test cases, test plans, test suites.**
  * Test suite -> Test Plans -> Test Cases
    ![image](https://github.com/user-attachments/assets/404a4123-ad8e-4efa-b86d-a9df292aba2c)'
  1. Subdivide system into features or subsystems
  2. For each feature, create a test plan with varied imputs + preconditions
  3. For each input + precondition, create a test case

* **Be able to critique an example test case on what problems it has.**
  * Problems with preciseness, reproducibility, independence.
* **Be able to tell problems with a test plan based on the traceability matrix.**
* **Be able to write a traceability matrix given requirements and test
  cases.**

## DEFECT REPORTING
* **Be able to explain the difference between a defect and a candidate for enhancement.**
  * Defect: When observed result != expected result
  * Candidate for enchancement: code/functionality that works but could be improved   
* **Be able to explain the difference between explicit and implicit requirements.**
  * Explicit requirements: requirements that are explicitly stated in the SRS
  * Implicit requirements: requirements not stated in the SRS but should be accounted for
    * EX: System shouldn't lose data when powered off, passwords should be encrypted in a database, etc.  
* **Be able to explain why implicit requirements make it sometimes hard to tell whether something is a defect or an enhancement.**
  * It depends on whether an implicit requirement was violated, if data is lost in a database when power is lost than it is a defect, but if its something like a game of solitaire then there is no expectation that the game will be saved on a power loss
  * All depends on the application domain, if an implicit requirement is not expected to be upheld for a piece of sotware, then it isn't a defect

* **Be able to explain why sometimes software is released with known bugs inside them.**
  * Bugs that are more severe will get tackled first before the deadline. If there are a lot of bugs to report and not enough time to fix them all, the bugs have the most critical implications are handled first and smaller bugs are handled later, or in future release
     
* **Be able to explain why bad coding style is not a defect.**
  * Defects are when observed != expected. Even if the coding style is bad, as long as observed == expected, then there is no defect
     
* **Be able to explain what triage and sub-triage are.**
  * A traige is when developers and stakeholders meet to discuss the severity of a bug and plan out how to handle it. They can determine whether the defect is valid or not, and if it is, they will assign someone to solve it
  * Open -> Assigned -> Resolved -> Verfied -> Closed
    * It's also possible to move backwards if any of the steps after open result in failure (test fail, unassigned) 

* **Be able to critique an example defect report on what problems it may have.**
  * Problems with preciseness and reproducibility.

## AUTOMATED TESTING
* **Be able to discuss in-depth of the pros and cons of automated testing.**
  * Why automated testing can be brittle and narrow.
    * Pros
      * Tests can run quickly and have less issues with reproducability
      * Additionally, they can catch defects the tests don't plan to catch
    * Cons
      * Brittle, can break easily and frequently due to changes in the codebase
      * Follow a rigid and strict path    
* Be able to explain what test automation looks like in a blackbox testing context and a whitebox testing context.

## UNIT TESTING
* Be able to list the 4 levels of testing in a hierarchy: acceptance/system/integration/unit.
* **Be able to write unit tests in JUnit given a test case.**
* **Be able to write integration tests in JUnit given a test case.**
* **Be able to write JUnit code to create stubs, test doubles, mocks,**
* **Be able to write JUnit code to perform both state verification and behavior verification.**
* Testing private methods
  * **Be able to discuss why/why not one might not decide to test them.**
    * Why not:
      *  Inacessable from external test class
      *  Get added/removed all the time
      *  tested as part of public methods anyways
    * Why to:
      * arbitrary distinction, deserve testing
      * can help localize a bug further   
  * **Be able to write code to test a private method using Java reflection.**
    * ![image](https://github.com/user-attachments/assets/c642cbaa-ce21-4523-b725-0b3b97f0de81)
 

## TDD
* **Be able to draw the red-green-refactor loop.**
  * **Be able to explain each of its components.**
    * Red - write a test for new functionality. Should fail immediately
    * Green - Implement enough code to make test pass
    * Refactor - review code and make it better 
* Be able to explain principles of TDD (including explaining acronyms):
  * **YAGNI** - You Ain't Gonna Need It
    * If the code isn't necessary for testing, then don't add it
  * **KISS** - Keep it simple, smarty pants
    * Less code = less possibility for errors
    * No need to overcomplicate or over engineer code 
  * **"Fake it 'til you make it"**
    * Dont get mired in writing code strictly not necessary to pass test 
  * **Avoid interdependency**
    * One test should not depend on the results of another tests 
  * **Avoid slow tests**
    * Test should be fast so more time is spent debugging then waiting to see if they pass or fail 
* **Be able to discuss the benefits and drawbacks of TDD**.
  * When to use it?
    * Coding effort is tightly bound to requirements
    * No regression
    * Small development increments 
  * When not to use it?
    * Tests can become overhead of the project
    * Limited creativity in architecture structure 

## BDD
* **Be able to discuss two problems in TDD that BDD solves.**
  * Hard to get feedback about requirements from stakeholders
    * Testing structure changes when requirements change, BDD allows stakeholders to be active in shaping requirements 
  * Hard to change requirements mid-development due to tests breaking
    * Behaviors are easily shared with stakeholders allowing for flexible tests structures that can be easily updated 
*** Be able to discuss drawbacks of BDD.**
  * Drawbacks of specification by example'
    * Leaves room for ambiguous requirements
    * Bad for backend safety/safety critical development 
* **Be able to take Gherkin and Cucumber code and trace through it and explain the end result.**
* **Be able to write Gherkin and Cucumber code given a test scenario, with reuse of Cucumber steps.**

## AUTOMATED (WEB) SYSTEMS TESTING
* **Be able to explain why testing a GUI web application involves a lot of text
  testing, just like text UI applications.**
    * HTML elements are, at the end of the day, just text componenets
    * GUI apps have text representation of the output
* **Be able to discuss reasons why testing an HTML verbatim against an expected
  HTML page is not desirable and how Selenium solves those problems.**
    * Trivial changes in HTML that doesnt impact final display can break tests
    * Chaning JS code that doesnt change functionality can also break tests
* Be able to explain why in Selenium, there is an option to select
  different locator strings for the same target element.
    * HTML elements are always changing, and some may be better for doing certain tests as they are less likely to change than others
* Be able to explain why race conditions occur and how to solve them.
  * Race conditions can occur due to varied respone times based on connection and when the user reacts, implicit waits can alleviate this by waiting a certain amount of time to do an action or wait until a certain element has loaded. 
