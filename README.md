# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Check on threshold changes if any
3. Information and details regarding the Notification mechanism - eg: mail - mail ID's 
4. Latest CSV file
5. Storage space


(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | We do not write SW to generate PDF report
Counting the breaches       | Yes           | This is one main task of analytics - part of SW
Detecting trends            | Yes           | This is one main task of analytics - part of SW
Notification utility        | No            | This is out of analytics scope

### List the Test Cases

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the count of breach to the PDF when readings cross thresholds
4. Write trends of date to the PDF when the readings increasing for more than 30 minutes
5. Write "Old record" to the PDF when the csv is older than a week
6. Write " CSV missing" to the PDF when CSV is not present
7. Write "PDF Report of BMS" to the notification in event of a new PDF
8. Write "Issues with PDF generation" to the notification in case of any technical issues in the course of PDF generation or earlier



(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                               | Faked/mocked part
|--------------------------|--------------|--------------------------------------|---
Read input from server     | csv file     | internal data-structure              | Fake the server store
Validate input             | csv data     | valid / invalid                      | None - it's a pure function
Notify report availability | PDF          | the notification mechanism trigger the message  |no receiver of the notification - it can be mocked 
Report inaccessible server | access denial message | report it via notification  | no receiver of the notification - it can be mocked 
Find minimum and maximum   | csv data     | the minimum and the maximum value    | None - it's a pure function
Detect trend               | csv data     | the detected trend                   | None - it's a pure function
Write to PDF               | processed analytics results | PDF                   | PDF generation 
