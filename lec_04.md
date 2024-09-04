# Lecture 4: Defects

## Defects and Enhancements

### Defects defined

* When observed behavior =/= expected behavior
* How do we know expected behavior? **Requirements!**

### Defects vs Enhancements

* Main job of a software QA team is to find and report defects
* But a QA team is also expected to find and suggest enhancements

* What is in common between defects and enhancements
  * Both involve modifications to software that can improve software quality
 
* What's the difference?
  * Defect: A violation of requirements
  * Enhancement: A Proposed improvement to existing requirements    

### Differentiating Defects vs Enhancements

* Differntiation is important as it can have legal implications
  * Defect: Developer must pay customer for damages
  * Enhacement: Customer may pay developer for the added improvement
 
* Differentiation between defects and enhancements due to implicit requirements

### Explicit vs Implicit Requirements

* Explicit requirement
  * A requirement taht is documented on the Software Requirements Specification (SRS)
  * Includes both functional and non-functional requirements
 
* Implicit requirement
  * A requirement not documented in the SRS but is still expected in the application domain
  * ex: databases should never store passwords unencrypted
 
* Even if the software does not violate the SRS, it is still a defect if it violates an implicit requirement
* Depends on the application domain

#### Understanding implicit requirements

* May need to do research on prior literature on the subject matter or talk to an expert of the subject matter ( or the customer ;) )

## Reporting Defects

### Typical bug report template

* **SUMMARY** - A one sentence description of the bug
* **DESCRIPTION** - details of the problem (don't overgeneralize)
* **REPRODUCTION STEPS** - Preconditions + Steps to reproduce Defect
  * First list all preconditions (if any)
  * then enumerate steps required to reproduce defect 
* **EXPECTED BEHAVIOR** - What you expect according to the requirements
  * describing expectations tells why observed behavior is deemed defective 
* **OBSERVED BEHAVIOR** - What you actually saw (be precise)
* **IMPACT** - impact to various stakeholders
* **SEVERITY** - How severe is the problem
  * How bad is the problem when it occurs, how often does it occur, and is there a workaround
  * Levels of severity
    * CRITICAL
    * MAJOR
    * NORMAL
    * MINOR
    * TRIVIAL 
* **PRIORITY** - ordering of defect resolution
  * Priority is about the ordering in which defects should be worked on first
  * Higher severity bug will be given a higher priority
 
## Tracking Defects

### Tracking Defects!

* Once defects are reported they need to be tracked so that they can be fixed in a timely manner
* Must be done in a systemic way
  * Like through a bug tracking system
 
* In order to track defects, we need the following info:
  * Identifier (numbered, not named)
  * Source: Associated test case
  * Version of software found
  * Version of software fixed

### Lifecycle of a defect

![image](https://github.com/user-attachments/assets/a112ac2e-d836-4fd8-b61f-56278f8fa464)

* Open
  * Defect ticked is first eneterd into the defect tracking system (either by software QA team or end-user)

* Assigned (Traige) - stakeholders meet to determing
  * 1. If the defect is not a valid defect (if not then close)
    2. If the defect is a duplicate (if so merge with previous ticket)
    3. Final severity and priority
    4. Assignment of defect to a particular developer
   
* Resolve (debug)
  * Assigned developer debugs effect
  * If not correct developer, unassign and reassign to different developer
 
* Verify (test)
  * Software QA team preforms various tests to verify fix
    * Regression test, performance test, security test, etc.
  * If any tests fail, reassign ticket back to developer
 
* Closed (close)
  * Close the defect ticket after verification is done
  * Closed ticket remains in the system for future reference

#### Make the defect lifecycle transparent to users

* It's normal for non-trivial software to ship with defects
* They should be advertised, not hidden
  
