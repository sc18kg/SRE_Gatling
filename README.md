# SRE Gatling
![overall](img/overall-diagram.png)
## What is Gatling
Gatling is a load testing tool which can be used for your integrated development environment, version control systems and continuous integration solutions. It does not have its own solution, rather it integrates with your existing solutions.  It is built on top of Akka, which is a toolkit for building distributed message driven applications. It is a distributed framework which will allow for fully asynchronous computing. It is a small entity within code communicating with each other through messaging.

## Gatling File Structure
----
```
+---bin
+---conf
+---lib
+---results
|   +---advancedsimulationstep05-20210920132657118
|   |   +---js
|   |   \---style
|   +---basicsimulation-20210920131556096
|   |   +---js
|   |   \---style
|   +---srekieronspartatest-20210920135455529
|   |   +---js
|   |   \---style
|   \---srekierontestappwithposts-20210920145438015
|       +---js
|       \---style
+---target
|   \---test-classes
|       \---computerdatabase
|           \---advanced
\---user-files
    +---resources
    \---simulations
        \---computerdatabase
            \---advanced
```
----
- `bin` contains the files such as `gatling.bat` and also `recorder.bat` which for windows users is the files used to create and record the gatling tests.
- `results` contains the outcomes of the tests in `.html` format which is used by inserting the full path to the file in your Google Chrome browser.
- `user-files` is the parent directory of `resources` and `simulations`
- `resources` contains
- `simulations` contains the `.scala` files which are created after the `recorder.bat` has been used and a `HAR file` has been input.

## What is Performance Testing
### Load Testing
A load test is a type of performance test that checks how systems function under a heavy number of concurrent virtual users performing transactions over a certain period of time. In other words, the test measures how systems handle heavy load volumes.

### Stress Testing
A stress test is a type of performance test that checks the upper limits of your system by testing it under extreme loads. Stress tests examine how the system behaves under intense loads and how it recovers when going back to normal usage. Are the KPIs like throughput and response time the same as before spike in load? Stress tests also look for memory leaks, slowdowns, security issues, and data corruption.

### Soak Testing
Soak testing (otherwise known as endurance testing, capacity testing, or longevity testing) involves testing the system to detect performance-related issues such as stability and response time by requesting the designed load on a system.
The system is then evaluated to see whether it could perform well under a significant load for an extended period, thereby measuring its reaction and analyzing its behavior under sustained use. Soak testing is a type of load testing.

### Spike Testing
Spike testing is a type of performance testing in which an application receives a sudden and extreme increase or decrease in load. The goal of spike testing is to determine the behavior of a software application when it receives extreme variations in traffic. Spike testing addresses more than just an application's maximum load; it also verifies an application's recovery time between activity spikes. The word “spike” refers to the sudden increase or decrease in traffic.

## User Experience/Journey
- Scalable
- Highly Available

## Steps to Complete Gatling Testing
### Recording the HAR file
1. Navigate to the HTTP which you would like perform testing on
2. Once at the designated page `right click` > `inspect` this should load up console either on the bottom or right side of the screen
3. Click the `Network` heading on the top bar
![inspect](img/inspect.png)
4. Tick the `Preserve log` and then move to the left where a circular stop sign which represents `clear` press this symbol
5. Perform the interactions which you would like to record and test
6. Once finished press `Export HAR` which is located just under the application header and is a down facing arrow
7. Save the file in a memorable location as this will need to be accessed for the next step

### Running the Tests
1. Head over to your `gatling-charts-highcharts-bundle` directory which I have defined the structure above
2. `cd bin` which will then show the `recorder.bat` file which now needs to be ran using `./recorder.bat`
3. This will bring up a screen we want to head over to the top-left corner to the `recorder` dropbox and select HAR
![harselect](img/recmode.png)
4. This will display the correct screen for us which is displayed below
![Correctscreen](img/recorderscreen.png)
5. We then select browse and locate the output file of our previous steps of recording the HAR file
6. On the right side of the screen, Name your file as this will be needed for a later step
7. Once thats loaded in, do NOT click anything other than `Start`
8. Navigate to your directory and you should see the created file with the name attached.
9. Run the command `./gatling.bat` and this should bring up a display.
```
Choose a simulation number:
     [0] RecordedSimulation
     [1] SreKieronSpartaTest
     [2] SreKieronSpartaTest2
     [3] SreKieronTestAppWithPosts
     [4] computerdatabase.BasicSimulation
     [5] computerdatabase.advanced.AdvancedSimulationStep01
     [6] computerdatabase.advanced.AdvancedSimulationStep02
     [7] computerdatabase.advanced.AdvancedSimulationStep03
     [8] computerdatabase.advanced.AdvancedSimulationStep04
     [9] computerdatabase.advanced.AdvancedSimulationStep05

```
10. Select the number and press enter
11. Write a description for the task 
12. Once complete an output `.html` file should be printed to the console, Paste this in your internet browser to view the results!

### Results
![Results](img/gatlingscreen.png)

## Editing The Tests
When creating the test from HAR files this creates a `.scala` file which is used to edit and modify the tests
```
class SreKieronTestAppWithPosts extends Simulation {

        val httpProtocol = http
                .baseUrl("http://34.243.55.216")
                .inferHtmlResources()

```
Here we see the `.baseUrl` which is used to tell the script what the target IP which is being tested.

### Changes to the Test
```
        setUp(scn.inject(atOnceUsers(1))).protocols(httpProtocol)
}
```
This line of code is at the end of the `.scala` file which is how you are able to change the injection of users by editing the number in the brackets from 1 to whatever value you are wanting.
