# Selenium with GitHub Copilot - Lab Instructions

## Lab Overview
In this hands-on lab, you'll learn how to write automated browser tests using Selenium WebDriver with TypeScript, while leveraging GitHub Copilot to accelerate your development workflow.

## Prerequisites
- Node.js (v16 or higher)
- Visual Studio Code
- GitHub Copilot extension installed
- Basic knowledge of TypeScript/JavaScript
- Chrome browser installed

## Lab Duration
Approximately 60-90 minutes

---

## Part 1: Project Setup (15 minutes)

### Step 1: Initialize the Project

1. Open VS Code and create a new folder for your project
2. Open the integrated terminal (`` Ctrl+` ``)
3. Initialize a new Node.js project:

```bash
npm init -y
```

### Step 2: Install Dependencies

Use Copilot to help you install the necessary packages. Type the following comment and let Copilot suggest the command:

```bash
npm install selenium-webdriver chromedriver
npm install --save-dev typescript @types/node @types/selenium-webdriver ts-node
npm install --save-dev @types/mocha mocha chai @types/chai
```

### Step 3: Configure TypeScript

Create a `tsconfig.json` file and use Copilot to generate the configuration:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

---

## Part 2: Create Base Configuration (15 minutes)

### Step 4: Setup WebDriver Utility

Create `src/utils/driver.ts` and use Copilot to generate the WebDriver setup:

1. Type the following comment: `// Create a utility class to manage Chrome WebDriver with proper setup and teardown`
2. Let Copilot suggest the implementation

**Expected Code:**

```typescript
import { Builder, WebDriver, Browser } from 'selenium-webdriver';
import * as chrome from 'selenium-webdriver/chrome';

export class DriverManager {
  private driver: WebDriver | null = null;

  async getDriver(): Promise<WebDriver> {
    if (!this.driver) {
      const options = new chrome.Options();
      options.addArguments('--start-maximized');
      options.addArguments('--disable-blink-features=AutomationControlled');
      
      this.driver = await new Builder()
        .forBrowser(Browser.CHROME)
        .setChromeOptions(options)
        .build();
    }
    return this.driver;
  }

  async quitDriver(): Promise<void> {
    if (this.driver) {
      await this.driver.quit();
      this.driver = null;
    }
  }
}
```

---

## Part 3: Implement Page Object Model (20 minutes)

### Step 5: Create Base Page Class

Create `src/pages/basePage.ts`:

1. Type: `// Create a base page class with common methods for all page objects`
2. Let Copilot generate the code

```typescript
import { WebDriver, By, until, WebElement } from 'selenium-webdriver';

export class BasePage {
  protected driver: WebDriver;
  protected timeout: number = 10000;

  constructor(driver: WebDriver) {
    this.driver = driver;
  }

  async navigate(url: string): Promise<void> {
    await this.driver.get(url);
  }

  async findElement(locator: By): Promise<WebElement> {
    await this.driver.wait(until.elementLocated(locator), this.timeout);
    return await this.driver.findElement(locator);
  }

  async click(locator: By): Promise<void> {
    const element = await this.findElement(locator);
    await element.click();
  }

  async sendKeys(locator: By, text: string): Promise<void> {
    const element = await this.findElement(locator);
    await element.clear();
    await element.sendKeys(text);
  }

  async getText(locator: By): Promise<string> {
    const element = await this.findElement(locator);
    return await element.getText();
  }

  async waitForElement(locator: By): Promise<WebElement> {
    return await this.driver.wait(until.elementLocated(locator), this.timeout);
  }

  async isElementPresent(locator: By): Promise<boolean> {
    try {
      await this.findElement(locator);
      return true;
    } catch (error) {
      return false;
    }
  }
}
```

### Step 6: Create a Sample Page Object

Create `src/pages/googlePage.ts`:

1. Type: `// Create a page object for Google search page with search functionality`
2. Use Copilot to complete the implementation

```typescript
import { By, WebDriver } from 'selenium-webdriver';
import { BasePage } from './basePage';

export class GooglePage extends BasePage {
  private searchBox = By.name('q');
  private searchButton = By.name('btnK');
  private results = By.id('search');

  constructor(driver: WebDriver) {
    super(driver);
  }

  async open(): Promise<void> {
    await this.navigate('https://www.google.com');
  }

  async search(query: string): Promise<void> {
    await this.sendKeys(this.searchBox, query);
    await this.click(this.searchButton);
  }

  async getSearchResults(): Promise<boolean> {
    try {
      await this.waitForElement(this.results);
      return true;
    } catch (error) {
      return false;
    }
  }

  async getPageTitle(): Promise<string> {
    return await this.driver.getTitle();
  }
}
```

---

## Part 4: Write Test Cases (20 minutes)

### Step 7: Create Your First Test

Create `src/tests/google.test.ts`:

1. Type: `// Create a test suite for Google search functionality using Mocha`
2. Let Copilot help you write the test

```typescript
import { describe, it, before, after } from 'mocha';
import { expect } from 'chai';
import { DriverManager } from '../utils/driver';
import { GooglePage } from '../pages/googlePage';
import { WebDriver } from 'selenium-webdriver';

describe('Google Search Tests', function() {
  this.timeout(30000);
  
  let driverManager: DriverManager;
  let driver: WebDriver;
  let googlePage: GooglePage;

  before(async function() {
    driverManager = new DriverManager();
    driver = await driverManager.getDriver();
    googlePage = new GooglePage(driver);
  });

  after(async function() {
    await driverManager.quitDriver();
  });

  it('should open Google homepage', async function() {
    await googlePage.open();
    const title = await driver.getTitle();
    expect(title).to.contain('Google');
  });

  it('should perform a search', async function() {
    await googlePage.open();
    await googlePage.search('Selenium WebDriver');
    const hasResults = await googlePage.getSearchResults();
    expect(hasResults).to.be.true;
  });

  it('should display search results for TypeScript', async function() {
    await googlePage.open();
    await googlePage.search('TypeScript');
    const hasResults = await googlePage.getSearchResults();
    expect(hasResults).to.be.true;
  });
});
```

### Step 8: Update package.json Scripts

Add test scripts to your `package.json`:

```json
{
  "name": "selenium-copilot-lab",
  "version": "1.0.0",
  "scripts": {
    "test": "mocha -r ts-node/register 'src/tests/**/*.test.ts'",
    "test:watch": "mocha -r ts-node/register 'src/tests/**/*.test.ts' --watch"
  }
}
```

---

## Part 5: Advanced Features with Copilot (15 minutes)

### Step 9: Use Copilot Chat for Test Ideas

1. Open Copilot Chat (`Ctrl+Alt+I`)
2. Ask: "Generate test cases for a login form with username and password fields"
3. Review and implement the suggestions

### Step 10: Generate a Login Page Object

Create `src/pages/loginPage.ts`:

1. Type: `// Create a login page object with username, password fields and submit button`
2. Let Copilot generate the implementation

```typescript
import { By, WebDriver } from 'selenium-webdriver';
import { BasePage } from './basePage';

export class LoginPage extends BasePage {
  private usernameField = By.id('username');
  private passwordField = By.id('password');
  private submitButton = By.css('button[type="submit"]');
  private errorMessage = By.className('error-message');

  constructor(driver: WebDriver) {
    super(driver);
  }

  async open(url: string): Promise<void> {
    await this.navigate(url);
  }

  async login(username: string, password: string): Promise<void> {
    await this.sendKeys(this.usernameField, username);
    await this.sendKeys(this.passwordField, password);
    await this.click(this.submitButton);
  }

  async getErrorMessage(): Promise<string> {
    return await this.getText(this.errorMessage);
  }

  async isErrorDisplayed(): Promise<boolean> {
    return await this.isElementPresent(this.errorMessage);
  }
}
```

### Step 11: Create Login Tests

Create `src/tests/login.test.ts`:

```typescript
import { describe, it, before, after } from 'mocha';
import { expect } from 'chai';
import { DriverManager } from '../utils/driver';
import { LoginPage } from '../pages/loginPage';
import { WebDriver } from 'selenium-webdriver';

describe('Login Tests', function() {
  this.timeout(30000);
  
  let driverManager: DriverManager;
  let driver: WebDriver;
  let loginPage: LoginPage;

  before(async function() {
    driverManager = new DriverManager();
    driver = await driverManager.getDriver();
    loginPage = new LoginPage(driver);
  });

  after(async function() {
    await driverManager.quitDriver();
  });

  it('should display error with invalid credentials', async function() {
    await loginPage.open('https://your-login-page.com');
    await loginPage.login('invalid@email.com', 'wrongpassword');
    const hasError = await loginPage.isErrorDisplayed();
    expect(hasError).to.be.true;
  });
});
```

---

## Part 6: Running and Debugging (10 minutes)

### Step 12: Run Your Tests

Execute tests from the terminal:

```bash
npm test
```

For watch mode:

```bash
npm run test:watch
```

### Step 13: Debug with Copilot

If tests fail:
1. Select the error in the terminal
2. Use Copilot Chat command: `/explain what happened in the terminal`
3. Ask Copilot: "How can I fix this Selenium timeout issue?"

### Step 14: Taking Screenshots on Failure

Use Copilot to add screenshot capability:

1. Type: `// Add method to take screenshot on test failure`
2. Update your test file with the suggested code

---

## Exercises

### Exercise 1: Form Testing
Create a test that:
- Navigates to a form
- Fills out multiple fields
- Submits the form
- Validates the result

**Hint**: Use Copilot by typing: `// Test form submission with validation`

### Exercise 2: Element Interactions
Create tests for:
- Dropdown selection
- Checkbox clicking
- Radio button selection
- File upload
- Taking screenshots

**Hint**: Ask Copilot Chat: "How do I handle dropdowns in Selenium?"

### Exercise 3: Waits and Synchronization
Implement different wait strategies:
- Implicit waits
- Explicit waits
- Custom wait conditions

**Example prompt for Copilot**: `// Implement custom wait for element to be clickable`

### Exercise 4: Data-Driven Testing
Create a test that:
- Reads test data from an array or JSON file
- Runs the same test with multiple datasets
- Reports results for each dataset

**Hint**: Ask Copilot: "How do I implement data-driven tests in Mocha?"



*Lab Version: 1.0*  
*Last Updated: December 2025*
