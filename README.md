# SRE Gatling

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
