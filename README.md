# 🚀 Selenium Parallel Automation Framework with Headless Support (Java + TestNG)

A **modern, scalable, and thread-safe Selenium automation framework** built using:

* Java
* Selenium WebDriver
* TestNG
* WebDriverManager

Designed for **parallel execution**, **clean architecture**, and **easy configuration management**.

---

## 📌 Key Features

* ⚡ Parallel execution with TestNG
* 🧵 Thread-safe WebDriver using `ThreadLocal`
* 🌐 Cross-browser and Headless support (Chrome, Firefox, Edge)
* ⚙️ Config-driven framework (`config.properties`)
* 🧪 Page Object Model (POM) design
* 📸 Automatic screenshot capture on failure
* 🔄 Data-driven testing using DataProvider
* 🧰 Built-in WebDriverManager support
* 🧼 Clean driver lifecycle management
* ❗ Robust custom exception handling

---

## 🏗️ Project Structure

```
com.amalw
│
├── base
│   └── BaseTest.java
│
├── config
│   └── ConfigManager.java
│
├── driver
│   ├── DriverFactory.java
│   └── BrowserManager.java
│
├── enums
│   └── BrowserType.java
│
├── exceptions
│   └── FrameworkException.java
│
├── pages
│   ├── BasePage.java
│   └── RegisterPage.java
│
├── tests
│   └── RegistrationTest.java
│
└── utils
    └── ScreenshotUtil.java
```

---

## ⚙️ Configuration

### 📄 `config.properties`

```properties
base.url=http://localhost:5000
browser=chrome
headless=true
timeout=30
```

---

### 🔁 Override via Command Line

```bash
mvn test -Dbrowser=firefox -Dheadless=true
```

> System properties override values from `config.properties`

---

## 🧠 Framework Architecture

This framework follows **Page Object Model (POM)** and **separation of concerns**.

---

### 🔹 ConfigManager

* Loads config using classpath (`/config.properties`)
* Supports system property overrides
* Provides:

  * `get()`
  * `getInt()`
  * `getBoolean()`
* Fails fast using `FrameworkException`

---

### 🔹 BrowserManager

Responsible for **creating WebDriver instances**.

* Uses `WebDriverManager`
* Supports:

  * Chrome
  * Firefox
  * Edge
* Handles **headless mode properly**
* Applies browser-specific options

```java
WebDriver driver = BrowserManager.createDriver(browser, headless);
```

---

### 🔹 DriverFactory

Handles **thread-safe WebDriver lifecycle**.

* Uses `ThreadLocal<WebDriver>`
* Delegates creation to `BrowserManager`
* Applies:

  * Page load timeout
  * Window maximize (only non-headless)
  * Zero implicit wait

```java
DriverFactory.initDriver("chrome");
WebDriver driver = DriverFactory.getDriver();
```

---

### 🔹 BasePage

Provides reusable Selenium actions:

* click()
* type()
* getText()
* navigateTo()
* wait utilities

Uses **explicit waits only (best practice)**.

---

### 🔹 Page Classes (RegisterPage)

* Encapsulates UI interactions
* Maintains locators + actions
* Returns page instance for chaining

---

### 🔹 BaseTest

* Initializes driver before each test
* Handles teardown after execution
* Captures screenshot on failure
* Keeps tests clean and minimal

---

### 🔹 ScreenshotUtil

* Captures screenshots on failure
* Stores in:

```
target/screenshots/
```

---

### 🔹 BrowserType Enum

* CHROME
* FIREFOX
* EDGE

Handles safe conversion from string → enum.

---

### 🔹 FrameworkException

Custom runtime exception used for:

* Missing config values
* Invalid browser
* Framework errors

---

## 🔄 Execution Flow

```
TestNG Test
   ↓
BaseTest (Setup / Teardown)
   ↓
DriverFactory (ThreadLocal)
   ↓
BrowserManager (Driver Creation)
   ↓
BasePage (Reusable Methods)
   ↓
Page Classes
   ↓
Selenium WebDriver
```

---

## 🧪 Test Execution

### 📄 TestNG (Parallel Execution)

* Parallel DataProvider enabled
* Thread-safe execution
* Cross-browser testing supported

---

## 🧾 Sample Test Flow

1. Initialize browser
2. Navigate to application
3. Perform UI actions
4. Submit form
5. Validate result
6. Capture screenshot if failure

---

## 🧪 Example Test

```java
@Test(dataProvider = "registrationData")
public void testRegistration(...) {

    RegisterPage page = new RegisterPage();

    page.open();
    page.selectGender(gender);
    page.fillForm(...);
    page.submit();

    Assert.assertTrue(page.isRegistrationSuccessful());
}
```

---

## 🚀 Running the Framework

### 📥 Clone Repo

```bash
git clone https://github.com/your-repo/selenium-parallel.git
```

---

### ▶️ Run Tests

```bash
mvn clean test
```

---

### 🌐 Run on Specific Browser

```bash
mvn test -Dbrowser=edge
```

---

### 🧪 Run in Headless Mode

```bash
mvn test -Dheadless=true
```

---

## 📸 Screenshot Example

```
target/screenshots/testName_timestamp.png
```

---

## 🧰 Tech Stack

* Java 17+
* Selenium WebDriver 4+
* TestNG
* Maven
* WebDriverManager


## 👨‍💻 Author

Designed for building scalable, maintainable, and parallel Selenium automation frameworks.
