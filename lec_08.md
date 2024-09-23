# Lecture 8 (09-23-24)

## Background

* Systems testing: Test the entire system as a whole
* Automated testing for CLI programs is easy

### Automated Systems Test for GUI programs 

* Not every program is a CLI program
  * Web pages, mobile applications, windows applications, etc.
 
* The theory behind testing remains the same
  * Compare observed behavior vs expected behavior
  * Preconditions
  * Execution steps
  * Postconditions
 
### Insight: GUI Apps ~ Text-based Apps 

* GUI apps also have text representation for the output
  * It's just that the text is rendered into a graphical representation for the end-user
 
* Example: Web Applications with HTML, Moblie applications with XML

### Testing a web app like a text-based app

1. HTML page is fetched from web server using wget
2. Fetched HTML page is compared against the expected HTML page

### Problem with Naive HTML Comparison

1. Tests are fragile
  * Trivial changes in HTML that don't impact final display can break test
2. Tests are untargeted
  * Changing HTML elements unrelated to test target will break test
3. JavaScript code is not functionally tested
  * JS code is compared verbatim to expected JS code, instead of executed
  * Changing in JS code that doesn't change functionality breaks test

* **All of these lead to false positive defects while testing**

## Solution: Web Testing Framework

* Web testing framework: framework for testing we apps at a semantic level
  * Robust: Works at DOM level after parsing HTML into a DOM tree
  * Targeted: Provides APIs to target individual HTML elements
  * Functionally tested
    * Provides APIs to call javascript code
    * Can emulate events like clicking or typing, which in turn invokes JavaScript code
   
### Web drives allows control of web browsers

* Web driver: An interface to control web browsers
  * Primarily intended to allow writing of automated tests
  * Also used to write scripts to automate repeated task
 
* Web browser writers implement drtiver for their own web browser
  * Matching web driver is used to test web app on a particular browser platform
 
## Selenium: A Web Testing Framework

* Selenium: open-source web testing framework
  * LIcensed under Apache License 2.0
  * Works with windows, OS X, Linux, other OSes
  * WOrks with Java, Ruby, Python, etc.
 
* Selenium = WebDriver + Grid + IDE
  * Selenium WebDriver: Drivers available for chrome and firefox
  * Selenium Grid: Grid computing service to run selenium tests in parallel
  * Selenium IDE: Browser extension for automated test script generation

### Selenium IDE

* What we would call a "test suite" 
