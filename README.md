# Factorial Calculator Tester

## Pre-requisites
- <a href="https://java.com/en/download/manual.jsp" target="_blank">Java</a>
- <a href="https://maven.apache.org/download.cgi" target="_blank">Maven</a>
  
## Setting up dotdata-factorial-tester
- Install Java and set JAVA_HOME
- Install Maven and set M2_HOME
- Extract dotdata-factorial-tester.zip

## Overview
 dotdata-factorial-tester is Cucumber-JVM based tool to test the web page http://qainterview.pythonanywhere.com/. The tests are based on Cucumber/Gherkin and the tools uses Selenium to run a headless browser to run these tests.

## Test Strategy
### Scope
Scope of this testing is to manually run the tests documented in [#Manual Tests] below and add Cucumber/Gherkin/Selenium based automation tests to run them on a headless browser. The list of automation test scenarios are documented in #Automation Tests section. Performance testing (Load/Stress) and Security testing is out of scope. 

### Test Environment
The Test Environment will include each of the supported browsers set up on supported Operating System(s)
### Test type
#### Functionality Testing
This will include validation and verification of the Factorial Calculator page for layout, content, links and input fields and form submission for +ve and -ve use cases.
#### Interface Testing
This will include testing the POST api http://qainterview.pythonanywhere.com/factorial for submitting the request with positive and negative data in param *number*
#### Compatibility Testing
Manual testing of features to test compatibilities related to browser, OS and devices (desktop, mobile etc)
#### User Acceptance Testing
Execute use cases for end to end and regression testing.
### Release Criteria and Failure Analysis
All the bugs shall be addressed and blocker must be fixed. An outcome with bugs still existing should be discussed with stakeholders before a decision is made.

## Manual Tests
1. Test output for various +ve inputs. Also verify that there is no latency in response

|Input|Expected Output|Status|
|--|--|--|
| 000000000000000000000000000000000000000000000000000000000000000000  |1|PASS|
|0|1|PASS|
|1|1|PASS|
|3|6|PASS|
|4|24|PASS|
|170|7.257415615307999e+306|PASS|

2. Test output for various -ve inputs

|Input|Expected message|Status|
|--|--|--|
|171|"Please enter an integer"|BUG: message is "The factorial of 171 is: Infinity"|
|"select * from users;"|"Please enter an integer"|PASS|
|"1a"|"Please enter an integer"|PASS|
|"a"|"Please enter an integer"|PASS|
|"-1"| "Please enter an integer"|BUG - Does not show any message. Api in Dev tools shows "500 Internal Server Error"|
| "111111111111111111111111111111111111111111111111111111111111111111111111111111111"|"Please enter an integer"|BUG - Does not show any message. Api in Dev tools shows "500 Internal Server Error"|

3. Test home page http://qainterview.pythonanywhere.com/ to verify the title and the layout. 

 - Verify the title. BUG: Title string has a typo. Expected "Factorial!". Actual: "Factoriall"
 - Verify the text "The greatest factorial calculator!" 
   - has letters in same case
   - in green font
   - is center aligned
   - is above the text box to enter number
 - Right arrow icon is visible at the left edge of the text box to enter number. It is not clickable
 - Text box to enter number is enabled with message "Enter an integer". You can select the text box
 - Submit buttle labeled "Calculate!" is visible below the text box 
 - No text between "Calculate!" button and links for "Terms and Conditions" and "Privacy"
 - Verify target links for "Terms and Conditions" and "Privacy". BUG: The links are swapped
 - Verify copyright content
   - It matches [copyright symbol] Qxf2 Services [Current Year]. BUG: Current Year is repeated (2020 - 2020)
   - Target link for text "Qxf2 Services' is valid
4. Change size of the browser window and verify that the layout is responsive
5. Test Factorial REST api using a tool like Postman or cURL from command line

## Automation Tests

The list of scenarios that part of automation tests are

1. Test output for various +ve inputs. Also verify that there is no latency in response

|Input|Expected Output|Status|
|--|--|--|
| 000000000000000000000000000000000000000000000000000000000000000000  |1|PASS|
|0|1|PASS|
|1|1|PASS|
|3|6|PASS|
|4|24|PASS|
|170|7.257415615307999e+306|PASS|

2. Test output for various -ve inputs

|Input|Expected message|Status|
|--|--|--|
|171|"Please enter an integer"|BUG: message is "The factorial of 171 is: Infinity"|
|"select * from users;"|"Please enter an integer"|PASS|
|"1a"|"Please enter an integer"|PASS|
|"a"|"Please enter an integer"|PASS|
|"-1"| "Please enter an integer"|FAIL|
| "111111111111111111111111111111111111111111111111111111111111111111111111111111111"|"Please enter an integer"|FAIL|

# Running the tests
- Goto dotdata-factorial-tester directory.
- Use "mvn test" command 
- Open target/result-html/index.html to see the test results
