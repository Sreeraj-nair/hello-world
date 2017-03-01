# Selenium WebDriver using Java Reference 

### What is Selenium WebDriver? 
Selenium is a set of tools and API that allows us to automate Browsers. 

### Browser platforms are supported by Selenium? 
Firefox, Internet Explorer, Google Chrome, Opera and Safari. 

### OS platforms supported by Selenium? 
Microsoft Windows 7, Apple OS X and Linux OS. 

### What are different language bindings available for Selenium? 
Programming languages are supported through Selenium "drivers". These are libraries made for each language that expose commands from the Selenium API natively in the form of methods/functions. 

### Lanuage bindings available with Selenium WebDriver? 
1. Java
2. C#
3. Ruby
4. Python
5. Javascript (Node)

### Testing Frameworks that can be used with Selenium. 
1. Java - JUnit, TestNG
2. C# - NUnit
3. Ruby - RSpec, Test::Unit
4. Python - Frameworks available: unittest, pyunit, py.test, robot framework
5. Javascript (Node) - WebDriverJS, WebdriverIO, NightwatchJS
6. PHP - Behat+Mink
7. Haskel
8. Objective C
9. Pearl

### What are different components of Selenium? 
Primarily, it can be divided into 3 parts -

1. Selenium IDE - Firefox browser plugin for recording and playback. Also can convert the recorded scripts to Java, C# and so on.

2. Selenium Standalone Server - For running Selenium scripts on remote or distributed machines. This would be required to run tests in      the Grid configuration.

3. Selenium WebDriver API. 

### What is the difference between Selenium and HP QTP? 
 
### What are different automation frameworks that can be created using Selenium WebDriver? 
1. Data Driven Test Automation Framework 
Test case logic resides in Test Scripts, test data is seperated and kept outside the test scripts. Test data is read from external files (Excel, CSV files) 

  | UserName  | Password |
  | ----------|----------|
  | ROBOT1    | robPass1 |
  | ROBOT2    | robPass2 |

2. Keyword or Table Driven Test Automation Framework
Most commonly used testing framework. Keyword is an action that can be performed on a GUI component. Eg. of an action is InputText, ClickButton, ClickCheckBox, ClickRadioButton, SelectValueFromDropdown and so on. 

  | ApplicationMap    | ActionKeyword   | Argument   |
  | ------------------|-----------------|------------|
  | textFieldUsername | inputText       | ROBOT1     |
  | submitButton      | clickButton     |            |

3. Hybrid Test Automation Framework 
It is the combination of one or more frameworks discussed above. 

4. Page Object Model Framework 
Page object model is a model that allows easy and quick maintenance. Application pages are physically seperated into different pages. Eg LoginPage.java, HomePage.java, UserRegistration.java, MenuBar.java. 
TestCase.java will contain the tests and will interact with the pages to execute tests. 

### What are the third party browser drivers available for Selenium? 
1. Mozilla GeckoDriver
2. Google ChromeDriver
3. HTMLUnitDriver
4. Appium
5. SafariDriver
6. ios-driver
7. InternetExplorerDriver is an exception 32-bit and 64-bit versions by SeleniumHQ. 

### What type of testing can be done using Selenium? 
    ### 1. Content Testing - This is the simplest type of test, a content test, is a simple test for the existance of a static, non-                changing UI element. For instance

              Does each page have its expected page title? This can be used to verify your test found an expected page after following a               link.        
              Does the application’s home page contain an image expected to be at the top of the page?
              Does each page of the website contain a footer area with links to the company contact page, privacy policy, and trademarks               information?
              Does each page begin with heading text using the \<h1> tag? And, does each page have the correct text within that header?

    ### 2. Testing links
              To find broken links. Testing involves clicking each link and verifying the expected page. If static links are not changed               frequently   then manual testing may be sufficient. However, if web designers frequently alter links, or if files are                   occationally relocated, link tests should be automated. 

### What are some of the important classes and interfaces of WebDriver? 

### How do you open a browser (FF/GC/IE) using Selenium WebDriver? 

### What are error collectors in Selenium? 

### How do you capture screenshots in Selenium? 

### How to do mouse hovering in Selenium? 

### How to automate browse and file upload using Selenium WebDriver? 

### How to automate drag and drop using Selenium WebDriver? 

### What are Web Services? 

### What is an XML? 

### What is JSON? 

### What are Restful or REST services? 

### What are SOAP services? 

## What is a WSDL? 

### Why do we need a web service? 

### What is JUnit and TestNG? 

### What is a page object model, explain with an example? 

### What are different element locators available in Selenium WebDriver? 

### What are different types of waits available in Selenium? 

### Which wait should be used for automation an app? 

### What's the difference between Verify and Assert in TestNG framework? 

### Explain the architecture of Selenium WebDriver? 

### What is Selenium Grid? 

### What is Robot API? 

### What is AutoIT API? 

### What is an Interface in Java? 

### What is an Abstract class in Java? 

### What is a concrete class or class in Java? 

### What is an object in Java? 

### What are various OOPS features available in Java? 

### How can you handle multiple windows in Selenium WebDriver? 

### Explain Exception handling in Java?




