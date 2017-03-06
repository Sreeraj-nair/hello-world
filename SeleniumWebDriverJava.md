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
      
### How to perform drag and drop in selenium? 
We can use dragAndDrop method provided by Action class of Selenium WebDriver. 

	Syntax
	
	WebDriver driver = new FirefoxDriver(); 
	
	Action action = new Actions(driver);
   
   	action.dragAndDrop(sourceLocator, destinationLocatior);

	Alternatively, the same code can can also be written as 
	
	(new Actions(driver)).dragAndDrop(source, targe).perform(); 

### How to set proxy for FF and IE? 
The easiest and recommended way is to manually set the proxy on the machine that will be running the test. 

However, you can do so programmatically for IE and FF like this. 

	Internet Explorer 
	
	String PROXY = "localhost";
	int PORT = 8080;

	com.google.gson.JsonObject json = new com.google.gson.JsonObject();
	json.addProperty("proxyType", "MANUAL");
	json.addProperty("httpProxy", PROXY);
	json.addProperty("httpProxyPort", PORT);
	json.addProperty("sslProxy", PROXY);
	json.addProperty("sslProxyPort", PORT);

	DesiredCapabilities cap = new DesiredCapabilities();
	cap.setCapability("proxy", json);

	GeckoDriverService service =new GeckoDriverService.Builder(firefoxBinary)
	  .usingDriverExecutable(new File("path to geckodriver"))
	  .usingAnyFreePort()
	  .usingAnyFreePort()
	  .build();
	service.start();

	// GeckoDriver currently needs the Proxy set in RequiredCapabilities
	driver = new FirefoxDriver(service, cap, cap);	

### How can you use FirefoxProfile. 
	FirefoxProfile fp = new FirefoxProfile();
	// set something on the profile...
	DesiredCapabilities dc = DesiredCapabilities.firefox();
	dc.setCapability(FirefoxDriver.PROFILE, fp);
	WebDriver driver = new RemoteWebDriver(dc);
	
### Element is not clickable error while executing Selenium scripts? 
Exception thrown: "org.openqa.selenium.WebDriverException: Element is not clickable at point (411, 675). Other element would receive the click: ..."

There are 3 reasons for this exception to occur - 
	1. The element is not visible to click. 
	You can use Actions or JavascriptExecutor for making it to click. 
	
	By Actions: 
	
		WebElement element = driver.findElement(By("element_path")); 
		
		Actions actions = new Actions(driver);
		
		actions.moveToElement(element).click().perform();
	
	By JavascriptExecutor 
	
		JavascriptExecutor jse = (JavascriptExecutor)driver;

		jse.executeScript("scroll(250, 0)"); // if the element is on top.

		jse.executeScript("scroll(0, 250)"); // if the element is on bottom.
	
	OR
	
		JavascriptExecutor jse = (JavascriptExecutor)driver;

		jse.executeScript("arguments[0].scrollIntoView()", Webelement); 
	
	Then click on the element. 
	
	2. The page is getting refreshed before it is clicking the element. 
	In this case make the page to wait for few seconds. 
	
	3. The element is clickable but there is a spinner or overlay on top of it. 
	In this case, code will wait until the spinner or overlay disappears. 
	
		By overlayImage = By.id("loadingOverlaySpanID");
		
		WebDriverWait wait = new WebDriverWait(driver, timeOutInSeconds);

		wait.until(ExpectedConditions.invisibilityOfElementLocated(loadingImage));
			
### What are error collectors in Selenium? 

### How do you capture screenshots in Selenium? 

### How to do mouse hovering in Selenium? 

### How to automate browse and file upload using Selenium WebDriver? 

### How to automate drag and drop using Selenium WebDriver? 

### What are Web Services? 

### What is an XML? 

### What is JSON? 
JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is a subset of JavaScript Programming Language. 
JSON is a text format that is completely language independent. These properties make JSON an ideal data-interchange language.

JSON is built on two structures: 
1. A collection of name value pairs. In various languages it is referred to as an object, record, struct, dictionary, hash table, keyed list, or associative array. 

2. An ordered list of values. Also realized as array, vector, list or sequence. 
These are universal data structures. Virtually all modern programming languages support them in one form or another. It makes sense that a data format that is interchangeable with programming languages also be based on these structures.

	object {string:value} 
	Where in each name is seperated by a colon : and every string value pair seperated by a coma ,
	
	array {value}
	Where each value is seperated by coma , 

### What are Restful or REST services? 

### What are SOAP services? 

### What is a WSDL? 

### Why do we need a web service? 

### What is JUnit and TestNG? 

### What is a page object model, explain with an example? 
Within the AUT there are areas the the tests interact with. There area are known as page objects. Reduces amount of duplicated code and means that if the UI changes, the fix needs to be applied on one place. 

POM can be thought of as facing in two directions simultaneously. Facing towards the developer of a test, they represent the services offered by a particular page. Facing away from the developer, they should be the only thing that has a deep knowledge of the structure of the HTML of a page. 
	
	public class LoginPage {
    		private final WebDriver driver;

    		public LoginPage(WebDriver driver) {
        	this.driver = driver;

        		// Check that we're on the right page.
        		if (!"Login".equals(driver.getTitle())) {
            		// Alternatively, we could navigate to the login page, perhaps logging out first
            		throw new IllegalStateException("This is not the login page");
        		}
    		}

	    	// The login page contains several HTML elements that will be represented as WebElements.
	    	// The locators for these elements should only be defined once.
		By usernameLocator = By.id("username");
		By passwordLocator = By.id("passwd");
		By loginButtonLocator = By.id("login");

	    	// The login page allows the user to type their username into the username field
    		public LoginPage typeUsername(String username) {
        	// This is the only place that "knows" how to enter a username
       		driver.findElement(usernameLocator).sendKeys(username);

        	// Return the current page object as this action doesn't navigate to a page represented by another PageObject
        	return this;    
    		}

    		// The login page allows the user to type their password into the password field
    		public LoginPage typePassword(String password) {
        	// This is the only place that "knows" how to enter a password
        	driver.findElement(passwordLocator).sendKeys(password);

        	// Return the current page object as this action doesn't navigate to a page represented by another PageObject
        	return this;    
    		}

    		// The login page allows the user to submit the login form
    		public HomePage submitLogin() {
       		// This is the only place that submits the login form and expects the destination to be the home page.
        	// A seperate method should be created for the instance of clicking login whilst expecting a login failure. 
        	driver.findElement(loginButtonLocator).submit();

        	// Return a new page object representing the destination. Should the login page ever
        	// go somewhere else (for example, a legal disclaimer) then changing the method signature
        	// for this method will mean that all tests that rely on this behaviour won't compile.
        	return new HomePage(driver);    
    		}

    		// The login page allows the user to submit the login form knowing that an invalid username and / or password were 			entered
    		public LoginPage submitLoginExpectingFailure() {
        	// This is the only place that submits the login form and expects the destination to be the login page due to login 			failure.
        	driver.findElement(loginButtonLocator).submit();

        	// Return a new page object representing the destination. Should the user ever be navigated to the home page after 			submiting a login with credentials 
        	// expected to fail login, the script will fail when it attempts to instantiate the LoginPage PageObject.
        	return new LoginPage(driver);   
    		}

    		// Conceptually, the login page offers the user the service of being able to "log into"
    		// the application using a user name and password. 
    		public HomePage loginAs(String username, String password) {
        	// The PageObject methods that enter username, password & submit login have already defined and should not be repeated 			here.
        	typeUsername(username);
        	typePassword(password);
        	return submitLogin();
    		}
	}

### What are different element locators available in Selenium WebDriver? 

### What are different types of waits available in Selenium? 
Waiting is having the automated task execution elapse a certain amout of time before continuing with the next step. You should choose to use Explicit or Implicit waits. 

	Waring: Should not mix both implicit and explicit waits. Doing so can cause unpredictable wait times. 

## 1. Explicit Waits 
An explicit wait will allow the automation task execution to wait for a certain condition to occur before proceeding further in the code. Worst case of this is Thread.sleep(), which sets the condition to an exact time period to wait. 

Using WebDriverWait in combination with ExpectedCondition is one way this can be accomplished. 

	Eg 1
	
	WebDriver driver = new FirefoxDriver();
	driver.get("http://url.com");
	WebElement myDynamicElement = (new WebDriverWait(driver, 10))
  	.until(ExpectedConditions.presenceOfElementLocated(By.id("myDynamicElement")));
	
	Eg 2 
	
	WebDriverWait wait = new WebDriverWait(driver, 10);
	WebElement element = wait.until(ExpectedConditions.elementToBeClickable(By.id("someid")));

## 2. Implicit Waits 
An implicit wait will tell WebDriver to poll the DOM for a certain amount of time when trying to find an element or elements if they are not immediately available. The default setting is 0. Once set, the implicit wait is set for the life of the WebDriver object instance.

	Eg 1. 
	
	WebDriver driver = new FirefoxDriver();
	driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
	driver.get("https://url.com");
	WebElement myDynamicElement = driver.findElement(By.id("someDynamicElement"));

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
An exception is an event that occurs during the execution of a program,that disrupts the normal flow of instructions. 

When an error occurs within a method, the method creates an object and hands it off to the runtime system. The object, called an exception object, contains information 

In java there are two exception types - Checked and Un-checked Exceptions. 

1. Checked exceptions are the ones checked at compile time. 

2. Unchecked exceptions are the ones that are not checked at compile time.  




