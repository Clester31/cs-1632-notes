# Lecture 11 (10/07/24)

## What is performance?

* In software QA, it is a non-functional requirement

### Speed is hard to quantify

* Even performance in the narrow sense (speed) is hard to quantify
* Speed for a web browser
  * How quickly a web page responds to user interactions
  * Speed is measured in response time
 
* Web server
  * How many pages the server can process per second
  * Measured in terms of throughput
  * Throughput != 1/response time due to parallel processing
 
* We need more than one metric to quantify perfomrance

### Performance Indicators

* Quantitative measures of the performance of a system under test
* Examples (in the narrow sense)
  * How long it takes to respond to a button press (response time)
  * How many users can the system handle at one time
 
* Examples (in the broad sense)
  * How long can the system go without a failure (availability)
  * How much memory is used in megabytes (memory efficiency)
  * How much energy is used per second in watts (energy efficiency)
 
### Key performance indicators

* KPI: performance indicator important to the user
* Select only a few KPIs that are really important
  * Those that are indicative of the success or failure of your software
  * ex: average response time (target: 100 ms, threshold: 500 ms)
  * ex: availability (more than 99.999% of HTTP requests serviced, threshold: 99.9%)
 
* Performance target: quantitative meaure KPI should reach ideally
* Performance threshold: minimum KPI that should be achieved

### Performance indicator categories

* Service oriented
* Effieciency oriented

#### Service oriented performance indicators

* Measures how well a system is providing a service to teh users
  * Measures how users experience your system, the QoS
  * Often codified in SLA (Service Leagl Agreement) between user and provider
 
* Subcategories
  * Response time
    * How quickly system responsds to a user requrest
    * How long a web page takes to load
  * Availability (uptime)
    * Percentage of time user's can accesss the services of the system
   
#### Efficiency oriented performance indicators

* Measures how efficiently system makes use of system resources
  * CPU time, memory space, battery life, network bandwith...
  * Not directly observed by user but impacts QoS if resource is limited
 
* Categories
  * Utilization
    * Given a workload, amount of resources a system uses
  * Throughput
    * Given certain resources, amount of workload system can handle per time unit
   
##### Impact on QoS

* CPU utilization
  * Number of CPU clock tickes needed to handle request
  * Translates to response time, given a certain number of CPUs within a certain clock rate
* Memory Utilization
  * Bytes of memory needed to handle request
  * Translates to availability, given a certain amount of memory and flood of requests
* Server Throughput
  * Maximum number of requests handled per second
  * Translates to both response time and availability, given a certain number of servers
 
### Rough Response Time Performance Targets

* < 0.1s: response time that feels instantaneous
* < 1s: response time required for flow of thought not to be interrupted
* < 10s: response time required for users to stay focused on application

### Problem with manual response times

* Limited accuracy: Cannot reliably tell sub second differences
* Labor intensive: time-consuming to measure all usage scenarios
* Black box: can only measure end-to-end response times
  * DB queries, calls to endpoints, file r/w requests cannot be measured
 
#### Response time testing relies on automated tools

* UNIX time command
* Real time is the response time

* System repsonse time always form a distribution
  * Other process can run while testing, taking up CPU time
  * Other processes can take up memory while testing
  * Network can experience traffic while testing from unrealted sources
 
### Minimizing and Dealing with Variability

* Eliminate all variables **other that the code under test**
  * Make sure you are running with same software/hardware configuration
  * Kill a processes in the machine other than the one you are testing
  * Remove all periodic scheduled jobs (e.g., anti-virus)
  * FIll memory / caches by doing several warm up runs of app before measuring
 
* Eevn after doing all of this there is still variability
  * Try mutliple times to get a statistical average
 
#### Long Tail Latency

* Typically, this is the type of latency distribution you will get
* Often the "long tail" is more important than the average latency

### Testing Availability

* DIfficult - not feasible to run a few "test years" before deploying
* Modeling usage and estimating uptime is the only feasible approach

* Metrics to model
  * MTBF: Mean Time Between Failures
  * MTTR: Mean Time To Repair
  * Availability: MTBF/(MTBF + MTTR)
 
#### Measuring MTTR and MTBF

* MTTR
  * Average time to reboot a machine
  * Average time to replace a hard disk
 
* MTBF
  * Depends on how much the system is stressed
  * Depends on the usage scenario
  * Measure MTBF for different usage scenarios
    * Calculates a wighted average for MTBF
   
#### Measuring MTBF with Load Testing

* Load testing
  * Given a load, how long can a system run without failing
  * Load is expressed in terms of concurrent requests / users
 
* Kinds of load testing:
  * Soak / Stability Test - Typical usage for extended periods of time
  * Stress Test - High levels of activity typically in short bursts
 
## Testing Efficiency-Oriented Systems

### Testing Throughput

* Throughput is number of events a system can handle in a given timeframe
* Examples
  * Packets per second
  * Pages per minute
  * Number of concurrent users

### Load Testing

* Load testing can also be used to test throughput
* Measures maximal load system can handle without degrading QoS
  * Increment events / second until response tome falls below performance target

#### Testing Utilization: Tools

* General purpose
  * Windows System - Task Manager
  * OS X - Activity Monitor
  * Unix Systems - top, iostat, sar, perf, time
 
### Measuring CPU Utilization

* Real time: "Actual": amount of time taken (wall clock time)
* User time: AMount of time uesr code executes on CPU
* System time: Amount of time kernel (OS) code executes on CPU
* Total time: user time + system time = CPU Utilization

* Real time != total time
  * Real time = total time + idle time
  * Idle time: time app is idling (not executing on CPU) waiting for some event
 
* Sometimes total time > real time

### What does each indicator imply?

* High proportion of user time?
  * Means a lot of time is spent running use (application) code
  * Need to optimize algorithm or use efficient data structure
     
* High proportion of kernel time?
  * Means a lot of time is spent in OS to handle system calls or interrupts
  * Need to reduce frequency of system calls or investigate source of interrupts
 
#### Other Utilization performance indicators

* Page faults – indicates high physical memory utilization
* Network packets discarded – indicates high network utilization
* Disk cache misses – indicates high hard disk utilization
* CPU cache misses – indicates high memory bandwidth utilization

# "Premature optimization is the root of all evil"
