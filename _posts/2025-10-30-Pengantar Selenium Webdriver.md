---
title: "Pengantar Selenium WebDriver"
author: 
date: 2025-10-30 10:00:00 +0700
categories: [Materi]
tags: [selenium, webdriver, automation, ui-testing, web-testing]
image:
  path: assets/images/post/Selenium Webdriver/selenium webdriver.png
  alt: Pengantar Selenium WebDriver
---

> Selenium WebDriver adalah framework open-source yang powerful untuk automating web browser interactions - memungkinkan testing aplikasi web secara efisien, konsisten, dan scalable.
{: .prompt-tip }

---

## <i class="fas fa-globe"></i> Apa itu Selenium?

**Selenium** adalah suite of tools yang didesain untuk automating web browsers. Dibuat pertama kali oleh Jason Huggins di ThoughtWorks pada tahun 2004, Selenium telah berkembang menjadi standar industri untuk web automation testing. Name "Selenium" dipilih sebagai joke - pada masa itu, Mercury Interactive adalah vendor tool testing yang dominan, dan Selenium adalah cure untuk Mercury poisoning dalam dunia kimia.

Bayangkan Anda memiliki robot yang bisa menggunakan browser web seperti manusia - mengklik tombol, mengisi form, navigasi antar halaman, dan memverifikasi konten. Itulah yang Selenium lakukan. Instead of manually testing setiap fitur aplikasi web berulang kali setelah setiap update, Anda bisa write automation scripts yang run tests automatically, saving waktu dan mengurangi human error.

### Komponen Selenium Suite

**Selenium IDE** - Browser extension (Chrome/Firefox) untuk record dan playback test interactions. Perfect untuk beginners atau quick prototyping. Anda bisa record user actions dan generate code dalam berbagai languages.

**Selenium WebDriver** - Core component yang provides API untuk control web browsers programmatically. Ini adalah yang paling widely used dan akan menjadi focus dari materi ini. WebDriver communicate langsung dengan browser, making tests more realistic dan reliable.

**Selenium Grid** - Tool untuk running tests in parallel across multiple machines dan browsers. Ini dramatically reduce test execution time - instead of running 100 tests sequentially (maybe 2 hours), Anda bisa run across 10 machines simultaneously (12 minutes).

**Selenium RC (Remote Control)** - Predecessor dari WebDriver, sekarang deprecated. Masih disebutkan untuk historical context tetapi should not be used untuk new projects.

---

## <i class="fas fa-code"></i> Apa itu Selenium WebDriver?

**Selenium WebDriver** adalah programming interface untuk creating dan executing test cases. Ia provides APIs dalam multiple programming languages (Java, Python, C#, JavaScript, Ruby) yang allow developers untuk write automation scripts that interact dengan web browsers.

WebDriver works dengan berkomunikasi langsung dengan browser melalui browser-specific drivers. Setiap browser (Chrome, Firefox, Edge, Safari) memiliki driver sendiri yang act sebagai bridge antara WebDriver code dan browser. Architecture ini makes tests more robust dan closer ke real user interactions dibanding older Selenium RC approach.

### Mengapa WebDriver?

**Direct Browser Control** - WebDriver communicate directly dengan browser, bukan through JavaScript injection seperti Selenium RC. Ini makes tests more reliable dan realistic.

**Multi-Browser Support** - Single test script bisa run di Chrome, Firefox, Edge, Safari dengan hanya change driver. Write once, test everywhere.

**Multi-Language Support** - Choose bahasa programming yang team already familiar dengan:

| Language | Binding | Community | Use Case |
|---|---|---|---|
| **Java** | Selenium Java | Largest | Enterprise, strong typing |
| **Python** | Selenium Python | Very Active | Rapid development, scripting |
| **C#** | Selenium C# | Active | .NET ecosystem |
| **JavaScript** | WebDriverJS | Growing | Node.js integration |
| **Ruby** | Selenium Ruby | Active | Clean syntax, RSpec |

**Real Browser Testing** - Tests run in actual browsers, bukan simulated environments. Ini catch browser-specific issues dan CSS/JavaScript problems.

**Integration Friendly** - Easily integrate dengan test frameworks (JUnit, TestNG, pytest), CI/CD tools (Jenkins, GitHub Actions), dan reporting tools.

---

## <i class="fas fa-cogs"></i> Arsitektur Selenium WebDriver

Understanding architecture membantu troubleshooting dan writing better tests.

### Component Architecture

```
Test Script (Your Code)
        ↓
Language Binding (e.g., Selenium Java)
        ↓
JSON Wire Protocol / W3C WebDriver Protocol
        ↓
Browser Driver (ChromeDriver, GeckoDriver, etc.)
        ↓
Actual Browser (Chrome, Firefox, etc.)
```

**1. Test Script** - Your automation code dalam chosen programming language. Contains test logic, assertions, dan element interactions.

**2. Language Binding** - Library yang provides API untuk your language. Contoh: `selenium-webdriver` package untuk Python, `org.openqa.selenium` untuk Java.

**3. WebDriver Protocol** - Standardized protocol untuk communication. Originally JSON Wire Protocol, now transitioning ke W3C WebDriver Protocol.

**4. Browser Driver** - Executable yang specific untuk each browser:
- **ChromeDriver** - untuk Google Chrome
- **GeckoDriver** - untuk Mozilla Firefox
- **EdgeDriver** - untuk Microsoft Edge
- **SafariDriver** - untuk Apple Safari (built-in di macOS)

**5. Browser** - Actual browser instance yang controlled oleh driver.

### Communication Flow

```java
// When you write:
driver.findElement(By.id("username")).sendKeys("testuser");

// What happens:
1. WebDriver API translate command ke HTTP request
2. Request sent ke browser driver
3. Driver execute command dalam browser
4. Browser perform action (type "testuser" in username field)
5. Response sent back through chain
6. Your code continues
```

---

## <i class="fas fa-download"></i> Setup dan Installation

Mari setup environment untuk Selenium WebDriver testing.

### Prerequisites

**Java Development Kit (JDK)**
```bash
# Check Java version
java -version

# Should be 8 or higher
```

**Python (jika menggunakan Python)**
```bash
# Check Python version
python --version

# Should be 3.7 or higher
```

**IDE atau Text Editor**
- IntelliJ IDEA (Java)
- PyCharm (Python)
- Visual Studio Code (any language)
- Eclipse (Java)

### Installation Steps

**1. Install Selenium Library**

*Python:*
```bash
pip install selenium
```

*Java (Maven):*
```xml
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.15.0</version>
</dependency>
```

*JavaScript (Node.js):*
```bash
npm install selenium-webdriver
```

**2. Download Browser Drivers**

**Option A: Manual Download**
- ChromeDriver: https://chromedriver.chromium.org/
- GeckoDriver (Firefox): https://github.com/mozilla/geckodriver/releases
- EdgeDriver: https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/

Download driver yang match dengan browser version Anda, extract, dan add ke system PATH.

**Option B: WebDriver Manager (Recommended)**

*Python:*
```bash
pip install webdriver-manager

# Usage in code:
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service

service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service)
```

*Java:*
```xml
<dependency>
    <groupId>io.github.bonigarcia</groupId>
    <artifactId>webdrivermanager</artifactId>
    <version>5.6.2</version>
</dependency>
```

```java
import io.github.bonigarcia.wdm.WebDriverManager;

WebDriverManager.chromedriver().setup();
WebDriver driver = new ChromeDriver();
```

WebDriver Manager automatically download correct driver version, saving manual effort.

### Verify Installation

**Python:**
```python
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://www.google.com")
print(driver.title)  # Should print "Google"
driver.quit()
```

**Java:**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class Test {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://www.google.com");
        System.out.println(driver.getTitle());  // Should print "Google"
        driver.quit();
    }
}
```

Jika browser opens dan navigates ke Google, installation successful! 🎉

---

## <i class="fas fa-search"></i> Locating Elements

Core dari Selenium testing adalah finding dan interacting dengan elements di web page. WebDriver provides multiple strategies untuk locate elements.

### Locator Strategies

**1. ID - Paling Reliable**
```python
# HTML: <input id="username" type="text">
element = driver.find_element(By.ID, "username")
```

ID should be unique dalam page, making it fastest dan most reliable locator. **Best choice** jika available.

**2. Name**
```python
# HTML: <input name="email" type="email">
element = driver.find_element(By.NAME, "email")
```

Useful untuk form fields yang have name attributes.

**3. Class Name**
```python
# HTML: <div class="error-message">Invalid input</div>
element = driver.find_element(By.CLASS_NAME, "error-message")
```

Use untuk locate elements by CSS class. Note: only works dengan single class name (not "error-message red").

**4. Tag Name**
```python
# HTML: <h1>Welcome</h1>
element = driver.find_element(By.TAG_NAME, "h1")
```

Locate by HTML tag. Less specific, often returns first match.

**5. Link Text**
```python
# HTML: <a href="/login">Login</a>
element = driver.find_element(By.LINK_TEXT, "Login")
```

Specific untuk `<a>` tags. Must match exact text.

**6. Partial Link Text**
```python
# HTML: <a href="/register">Register New Account</a>
element = driver.find_element(By.PARTIAL_LINK_TEXT, "Register")
```

Match partial text dalam link. Useful ketika link text dynamic atau long.

**7. CSS Selector - Powerful & Flexible**
```python
# HTML: <button class="btn primary" id="submit">Submit</button>

# By ID
element = driver.find_element(By.CSS_SELECTOR, "#submit")

# By class
element = driver.find_element(By.CSS_SELECTOR, ".btn.primary")

# By attribute
element = driver.find_element(By.CSS_SELECTOR, "button[type='submit']")

# Nested
element = driver.find_element(By.CSS_SELECTOR, "div.form > input[name='username']")
```

CSS selectors are powerful dan fast. Recommended untuk most scenarios.

**8. XPath - Most Powerful**
```python
# HTML: <input type="text" placeholder="Enter username">

# By attribute
element = driver.find_element(By.XPATH, "//input[@type='text']")

# By text content
element = driver.find_element(By.XPATH, "//button[text()='Submit']")

# Complex navigation
element = driver.find_element(By.XPATH, "//div[@class='form']//input[@name='username']")

# Parent navigation
element = driver.find_element(By.XPATH, "//input[@id='username']/parent::div")
```

XPath paling flexible tetapi can be slower dan more fragile. Use ketika CSS selector insufficient.

### Best Practices untuk Locators

| Priority | Locator | Reason |
|---|---|---|
| **1st** | ID | Unique, fast, reliable |
| **2nd** | Name | Often unique, semantic |
| **3rd** | CSS Selector | Powerful, fast, readable |
| **4th** | XPath | Maximum flexibility when needed |
| **Last** | Link Text, Tag Name | Fragile, not specific enough |

**Tips:**
- Prefer stable attributes (id, data-testid) over dynamic (classes that change)
- Avoid locators based on position (nth-child) - fragile when layout changes
- Use semantic attributes ketika possible
- Consider dengan development team untuk add test-specific attributes (data-testid)

---

## <i class="fas fa-hand-pointer"></i> Interacting dengan Elements

Setelah locate elements, Anda perlu interact dengan them.

### Common Actions

**1. Click**
```python
# Click button, link, checkbox, radio button
element = driver.find_element(By.ID, "submit-button")
element.click()
```

**2. Send Keys (Type Text)**
```python
# Type into input field
username_field = driver.find_element(By.ID, "username")
username_field.send_keys("testuser123")

# Clear existing text first
username_field.clear()
username_field.send_keys("newuser")

# Special keys
from selenium.webdriver.common.keys import Keys
search_box.send_keys("Selenium WebDriver")
search_box.send_keys(Keys.ENTER)
```

**3. Get Text**
```python
# Get visible text
error_msg = driver.find_element(By.CLASS_NAME, "error")
print(error_msg.text)  # "Invalid username or password"
```

**4. Get Attribute**
```python
# Get attribute value
link = driver.find_element(By.TAG_NAME, "a")
href = link.get_attribute("href")
placeholder = input_field.get_attribute("placeholder")
```

**5. Check State**
```python
# Is element displayed?
if element.is_displayed():
    element.click()

# Is element enabled?
if submit_button.is_enabled():
    submit_button.click()

# Is checkbox/radio selected?
if checkbox.is_selected():
    print("Checkbox is checked")
```

**6. Select from Dropdown**
```python
from selenium.webdriver.support.ui import Select

# HTML: <select id="country">
dropdown = Select(driver.find_element(By.ID, "country"))

# Select by visible text
dropdown.select_by_visible_text("Indonesia")

# Select by value
dropdown.select_by_value("ID")

# Select by index
dropdown.select_by_index(0)

# Get selected option
selected = dropdown.first_selected_option
print(selected.text)
```

**7. Handle Alerts**
```python
# Accept alert (click OK)
alert = driver.switch_to.alert
alert.accept()

# Dismiss alert (click Cancel)
alert.dismiss()

# Get alert text
alert_text = alert.text

# Send text to prompt
alert.send_keys("Input text")
alert.accept()
```

**8. Switch Frames/Windows**
```python
# Switch to iframe by index
driver.switch_to.frame(0)

# Switch to iframe by name/id
driver.switch_to.frame("iframe-name")

# Switch to iframe by WebElement
iframe = driver.find_element(By.TAG_NAME, "iframe")
driver.switch_to.frame(iframe)

# Switch back to main content
driver.switch_to.default_content()

# Switch to new window
driver.switch_to.window(driver.window_handles[1])
```

**9. Execute JavaScript**
```python
# Scroll to element
element = driver.find_element(By.ID, "footer")
driver.execute_script("arguments[0].scrollIntoView();", element)

# Click via JavaScript (bypass click interception)
driver.execute_script("arguments[0].click();", element)

# Get page title via JS
title = driver.execute_script("return document.title;")
```

---

## <i class="fas fa-clock"></i> Waits dan Synchronization

Web pages load asynchronously - elements mungkin not immediately available. Proper waiting strategies crucial untuk stable tests.

### Types of Waits

**1. Implicit Wait (Not Recommended)**
```python
# Wait up to 10 seconds untuk element location
driver.implicitly_wait(10)

# Now every find_element will wait up to 10 seconds
element = driver.find_element(By.ID, "dynamic-content")
```

**Cons:** Applies globally, can slow down tests unnecessarily, less control.

**2. Explicit Wait (Recommended)**
```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Wait up to 10 seconds untuk specific condition
wait = WebDriverWait(driver, 10)

# Wait for element to be present
element = wait.until(
    EC.presence_of_element_located((By.ID, "dynamic-content"))
)

# Wait for element to be clickable
submit = wait.until(
    EC.element_to_be_clickable((By.ID, "submit"))
)

# Wait for element to be visible
message = wait.until(
    EC.visibility_of_element_located((By.CLASS_NAME, "success"))
)

# Wait for title to contain text
wait.until(EC.title_contains("Dashboard"))

# Wait for URL to change
wait.until(EC.url_contains("/home"))
```

**3. Fluent Wait (Advanced)**
```python
from selenium.webdriver.support.ui import WebDriverWait

wait = WebDriverWait(
    driver, 
    timeout=30,              # Maximum wait time
    poll_frequency=1,        # Check every 1 second
    ignored_exceptions=[NoSuchElementException]
)

element = wait.until(
    EC.presence_of_element_located((By.ID, "ajax-content"))
)
```

**4. Sleep (Avoid!)**
```python
import time

# BAD PRACTICE - Fixed wait
time.sleep(5)  # Always waits 5 seconds, even if not needed
```

Sleep adalah bad practice karena:
- Wastes time (waits even if condition already met)
- Not reliable (might not wait long enough)
- Makes tests slower

### Common Expected Conditions

| Condition | When to Use |
|---|---|
| `presence_of_element_located` | Element exists in DOM (might not be visible) |
| `visibility_of_element_located` | Element visible (has height/width) |
| `element_to_be_clickable` | Element visible dan enabled |
| `invisibility_of_element_located` | Element not visible atau not in DOM |
| `text_to_be_present_in_element` | Specific text present in element |
| `alert_is_present` | Alert popup appears |
| `title_contains` | Page title contains text |
| `url_contains` | Current URL contains text |

---

## <i class="fas fa-graduation-cap"></i> Contoh Lengkap: Login Test

Mari kita buat comprehensive example untuk login functionality testing.

### Test Scenario

**Application:** https://www.saucedemo.com  
**Test:** Login dengan valid credentials dan verify successful login

### Python Implementation

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service
import time

class TestLogin:
    def setup_method(self):
        """Setup yang runs before each test"""
        service = Service(ChromeDriverManager().install())
        self.driver = webdriver.Chrome(service=service)
        self.driver.maximize_window()
        self.driver.get("https://www.saucedemo.com")
        self.wait = WebDriverWait(self.driver, 10)
    
    def teardown_method(self):
        """Cleanup yang runs after each test"""
        self.driver.quit()
    
    def test_successful_login(self):
        """Test login dengan valid credentials"""
        # Locate elements
        username = self.driver.find_element(By.ID, "user-name")
        password = self.driver.find_element(By.ID, "password")
        login_button = self.driver.find_element(By.ID, "login-button")
        
        # Perform actions
        username.send_keys("standard_user")
        password.send_keys("secret_sauce")
        login_button.click()
        
        # Wait for dashboard to load
        products_title = self.wait.until(
            EC.visibility_of_element_located((By.CLASS_NAME, "title"))
        )
        
        # Assertions
        assert products_title.text == "Products"
        assert "inventory" in self.driver.current_url
        
        # Verify logout button visible
        menu_button = self.driver.find_element(By.ID, "react-burger-menu-btn")
        assert menu_button.is_displayed()
        
        print("✓ Login successful test passed")
    
    def test_invalid_credentials(self):
        """Test login dengan invalid credentials"""
        username = self.driver.find_element(By.ID, "user-name")
        password = self.driver.find_element(By.ID, "password")
        login_button = self.driver.find_element(By.ID, "login-button")
        
        username.send_keys("invalid_user")
        password.send_keys("wrong_password")
        login_button.click()
        
        # Wait for error message
        error = self.wait.until(
            EC.visibility_of_element_located(
                (By.CSS_SELECTOR, "h3[data-test='error']")
            )
        )
        
        # Assertions
        assert "Epic sadface" in error.text
        assert "Username and password do not match" in error.text
        
        print("✓ Invalid credentials test passed")
    
    def test_locked_out_user(self):
        """Test login dengan locked out user"""
        username = self.driver.find_element(By.ID, "user-name")
        password = self.driver.find_element(By.ID, "password")
        login_button = self.driver.find_element(By.ID, "login-button")
        
        username.send_keys("locked_out_user")
        password.send_keys("secret_sauce")
        login_button.click()
        
        # Wait for error message
        error = self.wait.until(
            EC.visibility_of_element_located(
                (By.CSS_SELECTOR, "h3[data-test='error']")
            )
        )
        
        # Assertions
        assert "Sorry, this user has been locked out" in error.text
        
        print("✓ Locked out user test passed")

# Run tests
if __name__ == "__main__":
    test = TestLogin()
    
    test.setup_method()
    test.test_successful_login()
    test.teardown_method()
    
    test.setup_method()
    test.test_invalid_credentials()
    test.teardown_method()
    
    test.setup_method()
    test.test_locked_out_user()
    test.teardown_method()
```

### Java Implementation

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.openqa.selenium.support.ui.ExpectedConditions;
import io.github.bonigarcia.wdm.WebDriverManager;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;
import java.time.Duration;

public class LoginTest {
    private WebDriver driver;
    private WebDriverWait wait;
    
    @Before
    public void setUp() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
        driver.manage().window().maximize();
        driver.get("https://www.saucedemo.com");
        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
    }
    
    @After
    public void tearDown() {
        if (driver != null) {
            driver.quit();
        }
    }
    
    @Test
    public void testSuccessfulLogin() {
        // Locate elements
        WebElement username = driver.findElement(By.id("user-name"));
        WebElement password = driver.findElement(By.id("password"));
        WebElement loginButton = driver.findElement(By.id("login-button"));
        
        // Perform actions
        username.sendKeys("standard_user");
        password.sendKeys("secret_sauce");
        loginButton.click();
        
        // Wait and verify
        WebElement productsTitle = wait.until(
            ExpectedConditions.visibilityOfElementLocated(
                By.className("title")
            )
        );
        
        assertEquals("Products", productsTitle.getText());
        assertTrue(driver.getCurrentUrl().contains("inventory"));
        
        System.out.println("✓ Login successful test passed");
    }
    
    @Test
    public void testInvalidCredentials() {
        WebElement username = driver.findElement(By.id("user-name"));
        WebElement password = driver.findElement(By.id("password"));
        WebElement loginButton = driver.findElement(By.id("login-button"));
        
        username.sendKeys("invalid_user");
        password.sendKeys("wrong_password");
        loginButton.click();
        
        WebElement error = wait.until(
            ExpectedConditions.visibilityOfElementLocated(
                By.cssSelector("h3[data-test='error']")
            )
        );
        
        assertTrue(error.getText().contains("Epic sadface"));
        assertTrue(error.getText().contains("do not match"));
        
        System.out.println("✓ Invalid credentials test passed");
    }
}
```

---

## <i class="fas fa-layer-group"></i> Page Object Model (POM)

POM adalah design pattern yang improves test maintenance dan readability dengan separating page structure dari test logic.

### Without POM (Bad Practice)

```python
def test_login():
    driver.find_element(By.ID, "user-name").send_keys("standard_user")
    driver.find_element(By.ID, "password").send_keys("secret_sauce")
    driver.find_element(By.ID, "login-button").click()
    # Locators scattered throughout test
```

**Problems:**
- Duplication (same locators in multiple tests)
- Hard to maintain (if locator changes, update everywhere)
- Test logic mixed dengan page structure

### With POM (Best Practice)

**Page Object:**
```python
from selenium.webdriver.common.by import By

class LoginPage:
    # Locators
    USERNAME_INPUT = (By.ID, "user-name")
    PASSWORD_INPUT = (By.ID, "password")
    LOGIN_BUTTON = (By.ID, "login-button")
    ERROR_MESSAGE = (By.CSS_SELECTOR, "h3[data-test='error']")
    
    def __init__(self, driver):
        self.driver = driver
    
    def enter_username(self, username):
        self.driver.find_element(*self.USERNAME_INPUT).send_keys(username)
        return self
    
    def enter_password(self, password):
        self.driver.find_element(*self.PASSWORD_INPUT).send_keys(password)
        return self
    
    def click_login(self):
        self.driver.find_element(*self.LOGIN_BUTTON).click()
        return ProductsPage(self.driver)
    
    def login(self, username, password):
        """Convenience method untuk complete login"""
        self.enter_username(username)
        self.enter_password(password)
        return self.click_login()
    
    def get_error_message(self):
        return self.driver.find_element(*self.ERROR_MESSAGE).text

class ProductsPage:
    PRODUCTS_TITLE = (By.CLASS_NAME, "title")
    
    def __init__(self, driver):
        self.driver = driver
    
    def get_title(self):
        return self.driver.find_element(*self.PRODUCTS_TITLE).text
    
    def is_loaded(self):
        return "inventory" in self.driver.current_url
```

**Test Using POM:**
```python
def test_successful_login():
    login_page = LoginPage(driver)
    products_page = login_page.login("standard_user", "secret_sauce")
    
    assert products_page.get_title() == "Products"
    assert products_page.is_loaded()

def test_invalid_login():
    login_page = LoginPage(driver)
    login_page.login("invalid", "wrong")
    
    assert "do not match" in login_page.get_error_message()
```

**Benefits:**
- ✅ Single source of truth untuk locators
- ✅ Easy maintenance (change locator in one place)
- ✅ Readable tests (business logic clear)
- ✅ Reusable page actions
- ✅ Method chaining possible

---

## <i class="fas fa-tasks"></i> Test Framework Integration

Selenium works dengan popular test frameworks untuk better organization dan reporting.

### pytest (Python)

```python
import pytest
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service

@pytest.fixture(scope="function")
def driver():
    """Setup dan teardown driver untuk each test"""
    service = Service(ChromeDriverManager().install())
    driver = webdriver.Chrome(service=service)
    driver.maximize_window()
    yield driver
    driver.quit()

class TestLogin:
    def test_valid_login(self, driver):
        driver.get("https://www.saucedemo.com")
        # Test code...
        assert True
    
    def test_invalid_login(self, driver):
        driver.get("https://www.saucedemo.com")
        # Test code...
        assert True

# Run: pytest test_login.py -v
```

**pytest Features:**
- Fixtures untuk setup/teardown
- Parametrized tests
- Rich assertions
- Plugins ecosystem (pytest-html, pytest-xdist)

### TestNG (Java)

```java
import org.testng.annotations.*;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class LoginTest {
    private WebDriver driver;
    
    @BeforeMethod
    public void setUp() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
        driver.get("https://www.saucedemo.com");
    }
    
    @AfterMethod
    public void tearDown() {
        driver.quit();
    }
    
    @Test(priority = 1)
    public void testValidLogin() {
        // Test code...
        Assert.assertTrue(true);
    }
    
    @Test(priority = 2)
    public void testInvalidLogin() {
        // Test code...
        Assert.assertTrue(true);
    }
}
```

**TestNG Features:**
- Annotations untuk lifecycle
- Test priorities dan dependencies
- Parallel execution
- Data providers
- Rich reporting

---

## <i class="fas fa-rocket"></i> Advanced Techniques

### 1. Taking Screenshots

```python
# Screenshot pada failure
try:
    element = driver.find_element(By.ID, "missing-element")
except:
    driver.save_screenshot("error_screenshot.png")
    raise

# Screenshot specific element
element = driver.find_element(By.ID, "content")
element.screenshot("element_screenshot.png")
```

### 2. Handling Multiple Windows

```python
# Store original window
original_window = driver.current_window_handle

# Click link yang opens new window
driver.find_element(By.LINK_TEXT, "Open New Window").click()

# Wait for new window
wait.until(EC.number_of_windows_to_be(2))

# Switch to new window
for window in driver.window_handles:
    if window != original_window:
        driver.switch_to.window(window)
        break

# Work dalam new window
print(driver.title)

# Close new window dan switch back
driver.close()
driver.switch_to.window(original_window)
```

### 3. Drag and Drop

```python
from selenium.webdriver.common.action_chains import ActionChains

source = driver.find_element(By.ID, "draggable")
target = driver.find_element(By.ID, "droppable")

actions = ActionChains(driver)
actions.drag_and_drop(source, target).perform()
```

### 4. Hover Actions

```python
from selenium.webdriver.common.action_chains import ActionChains

element = driver.find_element(By.ID, "menu-item")
actions = ActionChains(driver)
actions.move_to_element(element).perform()

# Now submenu should be visible
submenu = driver.find_element(By.ID, "submenu")
submenu.click()
```

### 5. File Upload

```python
# Locate file input
file_input = driver.find_element(By.ID, "file-upload")

# Send file path
file_input.send_keys("/path/to/file.txt")

# Click upload button
driver.find_element(By.ID, "upload-button").click()
```

### 6. Browser Options

```python
from selenium.webdriver.chrome.options import Options

options = Options()

# Headless mode (no GUI)
options.add_argument("--headless")

# Window size
options.add_argument("--window-size=1920,1080")

# Disable notifications
options.add_argument("--disable-notifications")

# Disable GPU (useful untuk headless)
options.add_argument("--disable-gpu")

# User agent
options.add_argument("user-agent=Custom User Agent")

# Start maximized
options.add_argument("--start-maximized")

driver = webdriver.Chrome(options=options)
```

---

## <i class="fas fa-exclamation-triangle"></i> Common Issues dan Solutions

### Issue 1: Element Not Interactable

**Problem:** Element exists tetapi can't be clicked.

**Causes:**
- Element hidden atau covered
- Element not in viewport
- Page still loading

**Solutions:**
```python
# Wait for element to be clickable
wait.until(EC.element_to_be_clickable((By.ID, "button")))

# Scroll to element
element = driver.find_element(By.ID, "button")
driver.execute_script("arguments[0].scrollIntoView();", element)

# Click via JavaScript
driver.execute_script("arguments[0].click();", element)
```

### Issue 2: Stale Element Reference

**Problem:** Element located, but page refreshed atau element removed.

**Solution:**
```python
# Re-locate element
def safe_click(by, value):
    try:
        element = driver.find_element(by, value)
        element.click()
    except StaleElementReferenceException:
        element = driver.find_element(by, value)
        element.click()
```

### Issue 3: NoSuchElementException

**Problem:** Element not found.

**Solutions:**
```python
# Use explicit wait
wait.until(EC.presence_of_element_located((By.ID, "element")))

# Check if element exists
elements = driver.find_elements(By.ID, "element")
if len(elements) > 0:
    elements[0].click()

# Handle dengan try-except
try:
    element = driver.find_element(By.ID, "element")
except NoSuchElementException:
    print("Element not found")
```

### Issue 4: TimeoutException

**Problem:** Wait time exceeded.

**Solutions:**
```python
# Increase wait time
wait = WebDriverWait(driver, 30)  # 30 seconds

# More specific condition
wait.until(EC.visibility_of_element_located((By.ID, "element")))

# Catch dan handle
try:
    element = wait.until(EC.presence_of_element_located((By.ID, "element")))
except TimeoutException:
    print("Element did not appear in time")
    driver.save_screenshot("timeout_error.png")
```

---

## <i class="fas fa-lightbulb"></i> Best Practices

### Do's ✅

**Use Explicit Waits** - More reliable dan faster dari implicit waits atau sleeps.

**Implement Page Object Model** - Separates page structure dari test logic, easier maintenance.

**Take Screenshots on Failure** - Helps debugging ketika tests run dalam CI/CD.

**Use Unique Locators** - Prefer ID > Name > CSS > XPath untuk stability.

**Clean Up Resources** - Always quit driver dalam teardown atau finally block.

**Run Headless in CI/CD** - Faster execution, less resource intensive.

**Parameterize Tests** - Use data-driven testing untuk test multiple scenarios.

**Keep Tests Independent** - Each test should run standalone tanpa dependency.

### Don'ts ❌

**Don't Use Sleeps** - Use explicit waits instead untuk better performance.

**Don't Hardcode Data** - Use configuration files atau test data files.

**Don't Test Third-Party Sites** - Focus pada your application, not external sites.

**Don't Over-Use XPath** - Fragile dan slow, prefer CSS selectors.

**Don't Ignore Exceptions** - Handle errors properly, don't use bare except.

**Don't Make Tests Too Long** - Break into smaller, focused tests.

**Don't Forget Browser Compatibility** - Test across different browsers.

---

## <i class="fas fa-quote-left"></i> Kesimpulan Utama

> "Automation testing dengan Selenium bukan tentang replacing manual testers - it's tentang empowering them untuk focus pada exploratory testing dan complex scenarios while repetitive tasks handled efficiently."
{: .prompt-info }

**Ringkasan Penting:**

**Selenium adalah Industry Standard** - Dengan 15+ years development dan massive community support, Selenium adalah go-to tool untuk web automation testing. Multi-language dan multi-browser support makes it versatile untuk different team needs.

**WebDriver Architecture** - Understanding architecture membantu troubleshoot issues. Know component chain: Test Code → Language Binding → WebDriver Protocol → Browser Driver → Browser.

**Element Location adalah Foundation** - Master different locator strategies. Prefer stable, unique identifiers (ID, data-testid) over fragile selectors (XPath based on structure).

**Waits are Critical** - Proper synchronization through explicit waits ensures test stability. Avoid sleeps - they waste time dan make tests unreliable.

**Page Object Model Scales** - As test suite grows, POM becomes essential untuk maintainability. Initial investment dalam POM pays off quickly.

**Integration dengan Ecosystem** - Selenium works seamlessly dengan test frameworks (pytest, TestNG), CI/CD tools, dan reporting tools. Leverage these untuk professional test automation.

**Continuous Learning** - Web technologies evolve, best practices change. Stay updated dengan Selenium updates, new features (Selenium 4 brings W3C WebDriver protocol, relative locators, etc.).

1. **Right Tool untuk Web Testing** - Selenium excels untuk browser automation
2. **Proper Waits Essential** - Explicit waits over sleeps
3. **POM for Maintainability** - Scales dengan test suite growth
4. **Cross-Browser Testing** - Single script, multiple browsers
5. **CI/CD Integration** - Automate execution untuk continuous quality
6. **Community Support** - Large ecosystem, plenty resources

---

## <i class="fas fa-book-open"></i> Referensi & Bacaan Lanjutan

**Official Resources:**
- **Selenium Documentation** - https://www.selenium.dev/documentation/
- **Selenium Blog** - Latest updates dan best practices
- **W3C WebDriver Specification** - Standard protocol

**Buku Rekomendasi:**
- *Selenium WebDriver 3 Practical Guide* - Unmesh Gundecha
- *Selenium Testing Tools Cookbook* - Unmesh Gundecha
- *Test Automation using Selenium WebDriver with Java* - Navneesh Garg
- *Mastering Selenium WebDriver* - Mark Collin

**Online Courses:**
- **Test Automation University** - Free Selenium courses
- **Udemy** - Comprehensive Selenium courses
- **Pluralsight** - Selenium paths
- **YouTube** - Channels: Automation Step by Step, The Testing Academy

**Practice Sites:**
- **The-Internet** - https://the-internet.herokuapp.com/
- **SauceDemo** - https://www.saucedemo.com/
- **Automation Practice** - http://automationpractice.com/
- **UI Test Automation Playground** - http://uitestingplayground.com/

**Tools & Frameworks:**
- **Selenium IDE** - Browser record/playback
- **WebDriver Manager** - Auto driver management
- **Robot Framework** - Keyword-driven testing
- **Selenium Grid** - Parallel execution
- **BrowserStack/Sauce Labs** - Cloud testing platforms

**Communities:**
- **Selenium Users Group** - Google Groups discussions
- **Stack Overflow** - Tag: selenium
- **Reddit** - r/QualityAssurance, r/selenium
- **Ministry of Testing** - Community resources

---

<div class="text-center text-muted small mt-5">
  <p class="mb-1"><i class="fas fa-users me-2"></i><strong>Kelompok 7</strong> • Pekan 7</p>
  <p class="mb-0">Materi Pengantar Selenium WebDriver</p>
</div>