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
1. Testing static content
2. Testing links
3. Function Tests 
4. Testing Dynamic Elements
5. Ajax Tests

### How do automate all the links available on a page? 


### What are some of the important classes and interfaces of WebDriver? 

### How do you open a browser (FF/GC/IE) using Selenium WebDriver? 
Launch Firefox and navigate to https://www.google.com 
        
         System.setProperty("webdriver.gecko.driver", "\\lib\\drivers\\geckodriver.exe"); 
         
         WebDriver driver = new FirefoxDriver(); 
         driver.get("http://www.google.com");
         OR
         driver.navigate().to("http://xyz.com/abc/tag.php");

         WebDriver driver = new ChromeDriver(); 
         driver.get("https://www.google.com"); 
        
### How to perform file upload and browse using Selenium? 
Since Selenium won't have any inbuilt APIs to interact with Windows or the underlying OS file system, we need to make use of an external API or plugin to do this. 
For performing the file upload, we have two options. 
1. The first way of doing it by finding the element and typing the absolute path of the document into it.

# This method works only when the text field is visible and enabled
       
       Syntax
       
       WebElement textFieldFilePath = driver.findElement(By.name("fileUpload")); 
       
       element.sendKeys("C:\Users\Documents\filename.doc");
       
2. When there is no text box or input tag to send the file path using SendKeys method. That is when you have a customized browse button    and on click a Window popup appears and file to be uploaded needs to be selected using Windows controls. And we are aware that          Selenium will not support OS controls. 
   In this case we can using AutoIT (v3), which is a freeware which uses BASIC like scripting language for automating the Window GUI and
   general scripting. 
   We need to call the AutoIT script after clicking on the upload or browse button. Immediately after clicking the Upload button, the 
   the control should be transferred to AutoIT which takes care of uploading the file. 
   
# This method can be used for Windows PC.        
       
       Syntax
       
       Runtime.getRuntime().exec("AutoIT.exe file path");
       
       Runtime.getRuntime().exec("D:/fileupload.exe");
   
   AutoIT script should have the following - 

   Step 1: After clicking on the browse button, the cursor will mode to the window popup. 
   Depending on the browser, the windows pop up may have following names - 
   Mozilla FF - File Upload
   Chrome - Open
   IE 11 - Choose File to Upload
   
       WinWaitActive("File Upload")

   Step 2: When the window pop up is active, file path needs to be passed. 
   
        Send("Full path of the document to be uploaded")
        
   Step 3: After that we need to click the Open which will upload the file. 
   
        Send("{ENTER}")
        
3. There is a third method which uses Robot API to interact with the browse control using Keypad controls. 
   
       Syntax
       
        public static void setClipboardData(String string) {
		          
            //StringSelection is a class that can be used for copy and paste operations.
		          StringSelection stringSelection = new StringSelection(string);
		          
            Toolkit.getDefaultToolkit().getSystemClipboard().setContents(stringSelection, null);
		     }
       
       	public static void uploadFile(String fileLocation){
           
           setClipBoardData(fileLocation); 
           
           Robot robot = new Robot(); 
           
           //Press control key
           robot.keyPress(KeyEvent.VK_CONTROL);
           
           //Press V
           robot.keyPress(KeyEvent.VK_V); 
           
           //Press control key again
           robot.keyPress(KeyEvent.VK_CONTROL); 
           
           //Press Enter key 
           robot.keyPress(KeyEvent.VK_ENTER); 
           
           //Release enter key 
           robot.keyRelease(keyEvent.VK_ENTER); 
        
       }
      
   
   
         
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




