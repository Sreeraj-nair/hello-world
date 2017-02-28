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
   
   6. TestNG allows execution based on Groups. Eg. If you have two groups, Sanity and Regression and if you want to execute only Sanity      tests, this can be done using TestNG. 
   
   7. TestNG supports parallel test execution.

## Parallel Test Execution in TestNG 

The below testng.xml will execute the methods in parallel. The parameter thread-count=2 specifies the number of threads that will be executed. 

      <!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
      <suite name="ParalletTestSuite" parallel="methods" thread-count="2">
         <test name="SmokeTests">
            <classes>
               <class name="com.tests.TestClassName"/>
            </classes>
       </test>
      </suite>

The parallel attribute on the <suite> tag can take one of the following values: 

      1. <suite name="My suite" parallel="methods" thread-count="5">
      2. <suite name="My suite" parallel="tests" thread-count="5">
      3. <suite name="My suite" parallel="classes" thread-count="5">
      4. <suite name="My suite" parallel="instances" thread-count="5">
      
 If you want to invoke a test method from different threads. It can be done as - 
   
      @Test(threadPoolSize=3, invocationCount=10, timeOut=1000)
      public void testLogin(){
      }

Here the method testLogin() will be invoked 10 times from three different threads. Additionally, a time-out of test seconds guarantees that none of the threads will block on this thread forever. 

## Re-running failed tests using Selenium WebDriver 

Every time tests fail in a suite, TestNG creates a file called testng-failed.xml in the output directory. This XML file contains the necessary information to rerun only those methods that failed, allowing you to quickly reproduce the failures having to run the entirety of your tests. 

A typical session on the command prompt would look like -

         java -classpath testng.jar;%CLASSPATH% org.testng.TestNG -d test-outputs testng.xml
         
         java -classpath testng.jar;%CLASSPATH% org.testng.TestNG -d test-outputs test-outputs\testng-failed.xml
         
## Test methods, Test classes and Test Groups

### Test Methods - 
Test methods are annotated with @Test. Methods annotated with @Test that happen to return a value will be ignored, unless you set allow-return-values to true in your testng.xml:
      
      <suite allow-return-values="true">
      or
      <test allow-return-values="true">

### Test Groups - 
         
### Test Methods - 

## Dependencies in Test Methods

Use dependency when tests needs to be executed in a certain order. Eg - 
   - To make sure that a certain test method has completed and succeeded before running more test methods. 
   - To initialize your tests while wanting this initialization methods to be test methods as well (methods tagged with @Before/After      will not be part of the final report).

TestNG allows you to specify dependencies either with annotations or in XML.

## Dependencies with annotations - 

We can use the attributes dependsOnMethods or dependsOnGroups, found on @Test annotation. 

There are two types of dependencies - 
### 1. Hard Dependencies - All the methods you depend on must have run and succeeded. Atleast one failure will SKIP the tests. 
   
         @Test
         public void launchAUT() {}
 
         @Test(dependsOnMethods = { "launchAUT" })
         public void verifyLogin() {}

Here, verifyLogin is declared as depending on method launchAUT(), which guarantees that launchAUT() will always be invoked. 
   
You can also have methods that depend on entire groups. 
   
         @Test(groups = { "init" })
         public void serverStartedOk() {}
 
         @Test(groups = { "init" })
         public void setUpEnvironment() {}
 
         @Test(dependsOnGroups = { "init.*" })
         public void verifyLogin() {}
      
Here, verifyLogin() is delacared as depending on any groups matching the regular expression "init.*", which guarantees that the 
methods serverStartedOK() and initEnvironment() will always be invoked before verifyLogin(). 
      
### 2. Soft Dependencies - Always be run after the methods you depend on, even if some of them have failed. Can be acheived by adding 
"alwaysRun=true" in your @Test annotation. 

## Logging Reporters in TestNG 
The org.testng.IReporter interface only has one method:

      public void generateReport(List<ISuite> suites, String outputDirectory)

This method will be invoked by TestNG when all the suites have been run and you can inspect its parameters to access all the information on the run that was just completed.

## Important Listeners in TestNG

## 1. ITestNGListener

org.testng
### Interface ITestNGListener

public interface ITestNGListener
   This is a marker interface for all objects that can be passed as a listener argument.

## 2. ITestListener 
public interface ITestListener extends ITestNGListener

Method details 
void onTestStart(ITestResult result)

void onTestSuccess(ITestResult result)

void onTestFailure(ITestResult result)

void onTestSkipped(ITestResult result)

void onTestFailedButWithinSuccessPercentage(ITestResult result)

void onStart(ITestContext context)
   
void onFinish(ITestContext context)
   
## What are Factories in TestNG? 
Factory allows you to create tests dynamically. For eg. when you want to create a test method that will access a page on a web site several times, and you want to invoke it with different values. 
   
   public class TestAUT {
         @Test(parameters = { "number-of-times" })
         public void accessPage(int numberOfTimes) {
            while (numberOfTimes-- > 0) {
            // access the web page
            }
         }
   }
   
TestNG.xml file would look like - 
   
      <test name="T1">
         <parameter name="number-of-times" value="10"/>
            <class name= "TestAUT" />
         </test>
 
      <test name="T2">
         <parameter name="number-of-times" value="20"/>
            <class name= "TestAUT"/>
      </test>
 
      <test name="T3">
         <parameter name="number-of-times" value="30"/>
            <class name= "TestAUT"/>
      </test>


   


