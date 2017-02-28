# Selenium WebDriver Learnings and important concepts
## Selenium is a tool for automating browsers. 

Test automation has specific advantages for improving the long-term efficiency of a software team’s testing processes. Test automation supports:

- Frequent regression testing
- Rapid feedback to developers
- Virtually unlimited iterations of test case execution
- Support for Agile and extreme development methodologies
- Disciplined documentation of test cases
- Customized defect reporting
- Finding defects missed by manual testing

## Reporting framework for Selenium WebDriver. 
- JUnit (JUnit.org - Eclipse Public License)
- TestNG (TestNG.org - Apache 2.0 License) 

## Advantages of TestNG over JUnit. 
    1. In JUnit @BeforeClass and @AfterClass must be declared, which is not a constrain in TestNG. 
    2. More annotations are available. Eg @BeforeSuite, @AfterSuite, @BeforeTest, @AfterTest, @BeforeGroup and @AfterGroup
    3. In JUnit methods are tests are executed based on the order of the test method names. Whereas in TestNG test methods can be named as    desired and execution can be set using @Test(priority=0) 0 and higher integers. 
    4. In TestNG it is possible to specify dependency of one method on another. However, JUnit won't allow that. 
    5. TestNG allows grouping of test methods however, JUnit won't allow grouping of test methods. 
    6. TestNG allows execution based on Groups. Eg. If you have two groups, Sanity and Regression and if you want to execute only Sanity       tests, this can be done using TestNG. 
    7. TestNG supports parallel test execution.

