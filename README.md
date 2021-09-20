# SRE Gatling

## Gatling File Structure
----
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
4. Tick the `Preserve log` and then move to the left where a circular stop sign which represents `clear` press this symbol
5. Perform the interactions which you would like to record and test
6. Once finished press `Export HAR` which is located just under the application header and is a down facing arrow
7. Save the file in a memorable location as this will need to be accessed for the next step

### Running the Tests
1. Head over to your `gatling-charts-highcharts-bundle` directory which I have defined the structure above
2. `cd bin` which will then show the `recorder.bat` file which now needs to be ran using `./recorder.bat`
3. 
### Results
