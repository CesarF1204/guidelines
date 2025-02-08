# Test Driven Development
A software development approach where tests are written before the actual code. Automated testing is crucial for ensuring code reliability, scalability, and efficiency. It helps catch bugs early, reduces manual testing efforts, and ensures consistent application behavior across updates. 

## Automated Testing in Frontend
### 1. Steps on how to use Selenium IDE to create a frontend test.
**Selenium IDE**
is a part of the Selenium suite and was developed to speed up the creation of automation scrips. It's a rapid prototyping tool and can be used by engineers with no programming knowledge whatsoever. It is easy to use interface to build automated test scripts. You can records user interactions on the browser and exports them as a reusable script.

1. Download and install the [selenium IDE chrome extension](https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd?hl=en). Once installed, launch it by clicking its icon from the menu bar in your browser. 
    
    *Note: Make sure the IDE is enabled in your browser's extension settings. 
    You can get there quickly by typing the following into your address bar and hitting Enter.* 
    - *Chrome: chrome://extensions*
    - *Firefox: about:addons*

2. Upon launching the IDE you will be presented with a welcome dialog. 
This will give you quick access to the following options:

    * Record a new test in a new project
    * Open an existing project
    * Create a new project
    * Close the IDE

    *If this is your first time using the IDE (or you are starting a new project), then select the first option.*

3. After creating a new project you will be prompted to name it. You can add a new test by clicking the **+** symbol at the top of left side-bar menu (to the right of the **Tests** heading), naming it, and clicking **ADD**.

    Once added you can either input commands manually, or click the record icon in the top-right of the IDE.

4. Before recording test cases you need to provide ta base URL. The base URL is the URL of the application you are testing. It's something you set once and it gets used across all of the tests in this project. You can change it later if need-be.

5. Once base URL is provided you can either input commands manually, or click the record icon in the top-right of the IDE.

    Interact with the page and each of your actions will be recorded in the IDE. To **stop recording**, switch to the IDE window and click the recording icon.

6. While recording, right click the page and select "Selenium IDE". The menu will expand and show all the list of available commands that you can use to add more actions on your tests.
    
    Here are the most common selenium IDE commands:
    * **click** - Clicks on a target element (e.g., a link, button, checkbox, or radio button).
    * **open** - Opens a URL and waits for the page to load before proceeding. This accepts both relative and absolute URLs.
    * **pause** - Wait for the specified amount of time.
    * **close** - Closes the current window. There is no need to close the initial window, IDE will re-use it; closing it may cause a performance penalty on the test.
    * **assert element present** - Confirm that the target element is present somewhere on the page. The test will stop if the assert fails.
    * **assert text** - confirm that the text of an element contains the provided value. The test will stop if the assert fails.
    * **send keys** - Simulates keystroke events on the specified element, as though you typed the value key-by-key. 
    * **submit** - Submit the specified form. This is particularly useful for forms without submit buttons, e.g. single-input "Search" forms 

    If you want to check all available commands you can check it [here](https://www.selenium.dev/selenium-ide/docs/en/api/commands#submit).

7. To save everything you've just done in the IDE, click the save icon in the top-right corner of the IDE.

    It will prompt you to for a location and name of where to save the project. The end result is a single file with a .side extension.

    **Important Reminder:** Always save your project because once the IDE is forced closed, all your unsaved data will be wipe out.


## 2. Steps on exporting Selenium IDE test.
1. You can export either a test or suite of tests to WebDriver code by right-clicking on a test or a suite, selecting Export.

2. A modal will prompt and will ask the type of language you want to export.
    You can also check the "Include origin tracing code comments" and "Include step description as a separate comment" to add more documentations on your test file.

3. Click the export button. This will save a file containing the exported code for your target language to your browser's download directory.


## 3. Steps on running exported test using Selenium Webdriver.
**Selenium WebDriver**
is a web framework that permits you to execute cross-browser tests. This tool is used for automating web-based application testing to verify that it performs as expected.

### Node.js Apps
1. Run the command below to install the necessary node modules:
```javascript
npm install --save mocha selenium-webdriver chromedriver
```
2. Create a folder named “tests” in the project folder.
3. Create a folder named “frontend” under the tests folder.
4. Paste or move the exported test file (Export using JavaScript Mocha in Selenium
IDE) inside the frontend folder.
5. Open the terminal, go to the directory of the project folder where the app.js is found, then run the command below:
```javascript
./node_modules/mocha/bin/mocha/ tests/frontend
```
6. Update package.json to include the following, to run all test cases at once using "npm test" command on your terminal
```javascript
    "scripts": {
        "test": "NODE_ENV=development ./node_modules/.bin/mocha tests/frontend/*.test.js",
    },
```

Your test should run after this, as long as you properly installed the node modules. Also,
please make sure that the chromedriver version is compatible with your Google Chrome
version.

## 4. How to make selenium webdriver scripts faster.
1. Use fast selectors (Arranged by fastest to slowest).
    1. search by ID

        This works if the html element has the id attribute.
        It is the fastest locator as it uses the document.getElementById() javascript command which is optimized for all browsers.

    2. NAME selector

        This works if the element has a name attribute.

    3. CSS selector

        It is faster than XPATH but not as flexible.

    4. XPATH selector

        This is the most flexible strategy for building locators.

        But xpath selectors are the slowest of all as the browser dom of the web page needs to be traversed for finding the element.
2. Use fewer locators
    Keep the number of locators as low as possible especially if using XPATH.

    This goes together with keeping scripts focused and short.

3. Create atomic tests

    **Avoid testing too many things in a single script.**

    It is better to have more small scripts focused on one thing only than fewer big scripts that do too many things.

    * Each test should test a single tiny bit of functionality
    * Each test should have up to 20 steps.
    * Each test should run in under 10 seconds.
    * Having atomic test is very useful in case of failures.

    The failures are very clear about where the problem is.

    **Example**

    Lets assume that one of the scripts is called testSignupLoginChangePasswordLogout().

    This script checks 4 different things:

    1. Signup form works
    2. Login works
    3. Change password works
    4. Logout works

    If the script fails, which part has an error? Signup? Login? ChangePassword? Logout?

    Instead, we should use smaller and atomic scripts:

    1. testSignup()
    2. testLogin()
    3. testChangePassword()
    4. testLogout()
    
    If any of the smaller tests fails, it is very clear where the problem is.

4. Dont test the same functionality twice.

    Make sure that your scripts are not checking the same features over and over.

    If you checked that the login works correctly in one script, there is no benefit from checking it again in another script.

5. Write good tests

    Good tests are created by following a few simple rules: **Good written tests are fast tests.**

    * Eliminate step duplication
    * Keep the scripts independent
    * Write just enough steps to go from A to B in the quickest way possible
    * Remove steps that are not related to the final result

6. Use only explicit waits

    One of the best ways of making a script faster is by using only explicit waits.

    If your test scripts uses delays and implicit waits like this,

    ```javascript
    await driver.get(`${site_url}/autologin/37pPNU85FPpBG5X3rrfLRDxre2HqDffJ/m:2:5513:35619`);
    await driver.sleep(50000); // Waiting time needed to proceed on the next step.
    await driver.findElement(By.id("login_section"));
    ```
    replace them with explicit waits like this.

    ```javascript
    await driver.get(`${site_url}/autologin/37pPNU85FPpBG5X3rrfLRDxre2HqDffJ/m:2:5513:35619`);
    await driver.wait(until.elementLocated(By.id("login_section")), 30000);
    ```
    The script performance is better with **explicit waits as HTML elements are accessed as soon as they become available.**

    No additional waiting times are needed.

7. Use the chrome driver

    **If you need a real browser, use Chrome and the Chrome driver.**

    The Chrome browser is faster than IE, Firefox, Safari and Opera.

    The same is valid for the Chrome web driver.

    **Results of running the same script 10 times**

    ![Use the chrome driver](https://seleniumjavadotcom.files.wordpress.com/2015/07/7d233-browsers.png?w=528&h=640 "Use the chrome driver")
    

8. Use drivers for headless browsers

    If you dont need a real browser or you use continuous integration, **headless browsers and drivers can make your scripts faster.**

    A headless browser is a browser that does not have a user interface.

    Use this option to enable the headless browsers for chrome browser.
    ```javascript
    let chrome_options = new chrome.Options().headless().windowSize(screen);

    driver = await new Builder()
                .forBrowser('chrome')
                .setChromeOptions(chrome_options)
                .build();
    ```

9. Re-use the browser instance

    The setUp() method uses the @BeforeAfter annotation and runs before each test script.

    Its purpose is usually to create the driver object and open the browser window.

    The tearDown() method uses the @AfterEach annotation and runs after each test script.

    Its purpose is to destroy the driver object and close the browser window.

    Each test script is using its own browser instance when the @BeforeEach and @AfterEach are used:

    setUp() –> opens browser
    Test Script 1
    tearDown() –> closes browser

    setUp() –> opens browser
    Test Script 2
    tearDown() –> closes browser

    setUp() –> opens browser
    Test Script 3
    tearDown() –> closes browser

    setUp() –> opens browser
    Test Script 4
    tearDown() –> closes browser


    The browser  instance can be shared by all test scripts if we use different annotations:

    1. @Before instead of @BeforeEach for the setUp() method
    2. @After instead of @AfterEach for the tearDown() method

    In this case, the setUp() method does not run before each test script but just once before all test scripts.

    The tearDown() method runs once only after all test scripts.

    After each test script, the browser is not closed so the next script can re-use it:

    setUp() –> opens browser
    Test Script 1

    Test Script 2

    Test Script 3

    Test Script 4
    tearDown() –> closes browser

10. Do not load images in the web page
    Many site pages are very rich in images so they do not load fast in the browser.

    If the page loads faster in the browser, the script will be faster as well.

    **The page will load faster if no images are loaded.**

    Use this option to enable the headless browsers for chrome browser.
    ```javascript
    let chrome_options = new chrome.Options().headless().windowSize(screen);
    chrome_options.addArguments("--blink-settings=imagesEnabled=false"); /* Disable's loading of images. */

    driver = await new Builder()
                .forBrowser('chrome')
                .setChromeOptions(chrome_options)
                .build();
    ```
**Note: Always run unit tests locally BEFORE sending any Pull-requests. More test files and commands can be found [here](https://docs.google.com/spreadsheets/d/1SsRA3leUnXMZLHvpLIY6TC0I7OCrsl6nIXArUqjo63s/edit?pli=1#gid=0)**

* * *

## Useful Links

**Introduction to Selenium**
https://www.guru99.com/introduction-to-selenium.html

**Selenium Commands**
https://www.youtube.com/watch?v=m4KpTvEz3vg&t
https://www.selenium.dev/selenium-ide/docs/en/api/commands

**What is Xpath?** 
https://www.w3schools.com/xml/xml_xpath.asp
https://www.w3schools.com/xml/xpath_syntax.asp

**Xpath Cheat Sheet**
https://devhints.io/xpath
https://gist.github.com/LeCoupa/8c305ec8c713aad07b14

**Setting up Selenium in Ubuntu** 
https://medium.com/@muhammetenginar/selenium-nodejs-on-ubuntu-vm-18-04-chrome-78-x-bbbcb30d674e
***
<br>

## Automated Testing in Backend

### Mocha
Mocha is a feature-rich JavaScript test framework running on Node.js and in the browser, making asynchronous testing simple and fun.

1. Install Mocha globally using this command.
    ```javascript
    npm install -g mocha
    ```
2. Create a test.js in your project folder and copy the following test codes from Mocha documentation.
    ```javascript
    var assert = require('assert');
    describe('Array', function() {
        describe('#indexOf()', function() {
            it('should return -1 when the value is not present', function() {
            assert.equal([1, 2, 3].indexOf(4), -1);
            });
        });
    });
    ```

    **describe()** is simply a way to group our tests. It takes two arguments, the first is the name of the test group, and the second is a callback function.

    **it()** is used for an individual test case. It  takes two arguments, a string explaining what the test should do, and a callback function which contains our actual test:

    **Assertion library** is a tool to verify things are correct - It’s what actually verifies the test results.

3. Now run the test in the command line using `npm test` and you should get the following message:
    ```javascript
    Array
    #indexOf()
        ✓ should return -1 when the value is not present

    1 passing (9ms)
    ```
You have now successfully run a PASSED mocha test. You can learn more about mocha [here](https://mochajs.org/)

### Chai
Chai is an assertion library. Above, we used Node's built-in assert library to make assertions. Chai does the exact same thing but allows for better readability.

1. First, Let's install Chai.
    ```javascript
    npm install --save-dev chai
    ```
2. Let's modify the our Mocha test to include chai:
    ```javascript
    var assert = require('assert');
    describe('Array', function() {
        describe('#indexOf()', function() {
            it('should return -1 when the value is not present', function() {
                let param_1 = [1, 2, 3].indexOf(4);
                let param_2 = -1;
                expect(param_1).to.equal(param_2);
            });
        });
    });
    ```
3. Now run the test in the command line using `npm test` and you should get the following message:
    ```javascript
    Array
    #indexOf()
        ✓ should return -1 when the value is not present

    1 passing (9ms)
    ```
    
*Note: When running unit tests locally, we advise to open Git Bash (to avoid syntax error when using Windows) and type the ff. as example:*
```sh
cd <project path>
npm run build  #this will create dist-server folder compiled by Babel which may take longer time
NODE_ENV=development ./node_modules/.bin/mocha dist-server/test/certificates/certificates.test.js
```
**NOTE: Always run unit tests locally BEFORE sending any Pull-requests. More test files and commands can be found [here](https://docs.google.com/spreadsheets/d/1SsRA3leUnXMZLHvpLIY6TC0I7OCrsl6nIXArUqjo63s/edit?pli=1#gid=0)**


### Zombie
Zombie.js is a lightweight framework for testing client-side JavaScript code in a simulated environment. No browser required.


1. To install Zombie.js you will need Node.js:
    ```javascript
    npm install zombie --save-dev
    ```
2. Create a test file and paster this code. Check the comments for detailed info.
    ```javascript
    const Browser = require('zombie');

    // We're going to make requests to http://example.com/signup
    // Which will be routed to our test server localhost:3000
    Browser.localhost('example.com', 3000);

    describe('User visits signup page', function() {
        const browser = new Browser();

        before(function(done) {
            // This will visit the /signup page before entering the first test.
            browser.visit('/signup', done);
        });

        describe('submits form', function() {
            before(function(done) {
                // This will fill up the email and password
                browser
                    .fill('email',    'zombie@underworld.dead')
                    .fill('password', 'eat-the-living')
                    .pressButton('Sign Me Up!', done);
                // And submits the form
            });

            it('should be successful', function() {
                browser.assert.success();
            });

            it('should see welcome page', function() {
                browser.assert.text('title', 'Welcome To Brains Depot');
            });
        });
    });
    ```
    This example uses the Mocha testing framework, but Zombie will work with other testing frameworks. Since Mocha supports promises, we can also write the test like this:

    You can check the list of **Browser methods** [here](http://zombie.js.org/#browser);

3. Now run the test in the command line using `npm test` and you should get the following message:
    ```javascript
    Array
    #indexOf()
        ✓ should return -1 when the value is not present

    1 passing (9ms)
    ```