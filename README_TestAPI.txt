JMeter
How run the test
1. Download JMeter 5.1.1 from official site: https://jmeter.apache.org/download_jmeter.cgi
2. At least, java 8 is requiered. Unzip and execute jmeter.bat/jmeter.sh
3. Open the file "TestAPI.jmx".
4. "Play" (green button) to run the tests. Mouse has to be on the root to run all tests.
5. Results are avaible on both (same results in two formats):
5.1 JMeter: I've added "View ResultsTree" (to check response) and "View Results in table" (as summary) to track the results. I've added too "Assertion Results to check the value of each assertion.
5.2 Files are generated with the results: One for the results (TestAPI_*Cities), One for assertions (TestAPI_Assertions_*). 
Some files are provided as example of execution. Warning: If you execute the test, be carefull choosing "add results" (in the pop-up window) not to override the current files: TestAPI_OneCities.csv, TestAPI_ErrorCases.csv, TestAPI_Assertions_ServeralCities.csv, TestAPI_Assertions_OneCities.csv, TestAPI_Assertions_Errors.csv.

Why JMeter?
I've never used Cucumber or other tool for BDD. 
My knowledge about BDD is very limited but I know quite well JMeter and this tool can test front and backend in other way.
JMeter can be useful for overload test too (In these examples only one thread has been used).

Why this design test?
I've created test for several calls as example (not all of them, there are too much ;-))

Test Suite - Test API Current Weather: I've created a global variable SERVER having the URL base to test (easy to change, instead of using a different one for each test).
--> One city APIs: A group for "One city" calls:
- HTTP Request Defaults: Common data for all calls (protocol, server, path, appid)
- HTTP Request: I've created calls to use "by name", "by city id", "by geographic coordinates", "by zip" (there are more in the API doc,but I think is enough as example). Each HTTP request uses its own parameters to call the API without errors. The first one ("By name") has several assertions as example: Code response is ok (=200), No "ERROR" in response text and two assertions to check coordinates and weather are in the text response. We could add more assertiond to check all data are in the response. And the other test cases should have similar assertions.

--> Several Cities: A group for "Several cities" calls:
- HTTP Request Defaults: Common data for all calls (protocol, server, appid)
- HTTP Request: I've created calls to use "within a rectangle zone", "cities in cycle", "cities by ids" (there are more in the API doc,but I think is enough as example). Each HTTP request use its own parameters and without errors. Assertions should been added in a similar way as One city by name example.

--> One city - Error cases: This is a group to check the errors are returned with the right code. It has been done as example for "one city" call for 401 error (not authorized, using an invalid API key) and other errors (4xx or 5xx codes).

