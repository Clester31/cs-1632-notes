# Lecture 7 - Behavior Driven Development

## Waterfall Model

* Linear sequential approach to do development

![image](https://github.com/user-attachments/assets/c566649c-c45b-4bfb-90bf-cd085531d495)

## Agile Software Development: Quick adaptation to changing requirements

* Agile: A development process amenable to frequent changes in requirement
  * Stresses adapting to user needs quickly vs negotiating a contract
  * Stresses efficient communication vs. comprehensive specification
  * Stresses iterative design vs rigid plan
 
* Some Agile practices
  * Continuous Delivery (CD)
    * Frequent Delivery of software for user feedback
   
  * Test Driven Development (TDD)
    * Allows continuous delivery through continuousl testing
   
  * **Behavior Driven Development (BDD)**
    * A type of TDD better suited for adapting to user needs
   
### TDD Strength: Coding is driven by requirements

* Requirements drives -> testing drives -> Development
  * Test cases are written based on the requirements
  * Code is written to fulfil the test cases
 
* End Result:
  * Ensures all code adheres to requirements at all times
  * Ensures all coding effort is focused on fulfilling requirements
 
### TDD Weak Link 1:

* Typical Software Requirements Specifications (SRS)
  
  ![image](https://github.com/user-attachments/assets/4a3eb5b5-d297-4546-85a7-5c2b7793e9f7)

* Very long, end-users will not want to read it
* Even if they did read it they would not understand it

* SRS is not meant to be read by the end user
  * Meant for lawyers: SRS is a contract
  * Meant for developers: SRS is a specification
* Painstakingly compiled by requirements analysis after interviewing stakeholders

* But what if requirements must change often?
* Now SRS becomes a burden:
  * End-user must pore through SRS in order to give feedback
  * Hundreds of pages of SRS documents must be maintained throughout
* SRS should be a tool for communication with user, not litigation

### TDD Weak Link 2:

* Maintaining test cases can become a burdern

* If requirements change often, since Requirements -> Tests -> Code
  * Testing infrastructure needs to change often as well
 
* TDD means a lot of time is spent maintinging testing infrastructure
  * Time that would not be spent had we not done TDD
  * Maintianing testing infrastructure can be extra baggage
  * Testing should improve productivity, not decrease it
 
## Behavior Driven Development (BDD): Behavior is Requirements and Test in one

* Paradigms laid down by Dan North:
  * Software is described in terms of behaviors not code-centric specifications
  * Behaviors are in a "ubiquitous language" --- in other words plain english
  * Behaviors are "execuatable" --- behaviors are directly testable on the code
      
### Behavior-Driven Development: Solves existing problems with TDD

* Maintaining requirements can become a burden
  * Behaviors are easily shared with and updated by the stakeholders
 
* Maintaining test cases can become a burden
  * Since behaviors are the tests, tests are upadted with requirements
 
* Closer to the Agile philosophy of adapting to user needs
  * Now stakeholders become active participants in shaping requirements
  * Now software companies are not as afraid to change requirements

### Dialect for Describing Behaviors: Gherkin or JBehave

* Dialect for describing behaviors must satisfy two criteria
  * Must be like plain english so end-users can understand it
  * Must have some structure so testing behaviors can be automated
 
* Two populat doman specific languages
  * Gherking: Used with Cucumber testing framework
  * JBehave: Used with the JBehave testing framework
 
#### Gherkin Hieratchy

* Feature - a descrite functionality or subsystem (user story)
* Rules - One or more business ruels that a feature must follow
* Scenario - One or more use cases that demonstrate a rule
* Steps - Preconitions, execution steps, postconditions for a scenario

#### Feature Syntax

* Feature: <text>
  * <text> can be any multi-line text that extends until the next keyword
 
* A <text> is usally a one line descriptino of the feature followed by
  * As a <role>
  * I want <function>
  * so that <reason / benefit>
    * <role>: User administrator, customer service, data analyst
    * <function>: what functionality the feature provides
    * <benefit>: What business goals the function serves for this role 
