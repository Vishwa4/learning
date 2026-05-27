-> Playwright is a modern, open-source end-to-end (E2E) test automation framework developed by Microsoft. It allows you to automate browser interactions for testing web applications across multiple browsers.


# Core Concepts
### Page Object Model (POM)
The pattern you're using! Separates page element definitions from test logic.
```
// pages/LoginPage.js
export class LoginPage {
  constructor(page) {
    this.page        = page;
    this.emailInput  = page.locator("//input[@name='email']");
    this.passwordInput = page.locator("//input[@name='password']");
    this.loginButton = page.locator("//button[@type='submit']");
  }

  async login(email, password) {
    await this.emailInput.fill(email);
    await this.passwordInput.fill(password);
    await this.loginButton.click();
  }
}
```

### Locators
Ways to find elements on the page:
```
// By XPath
page.locator("//input[@name='email']")

// By CSS selector
page.locator("input[name='email']")

// By text
page.getByText('Submit')

// By role
page.getByRole('button', { name: 'Save' })

// By placeholder
page.getByPlaceholder('Enter your name')

// By label
page.getByLabel('Email address')

// By test ID
page.getByTestId('submit-btn')
```

### Assertions (expect)
```
import { expect } from '@playwright/test';

// Visibility
await expect(locator).toBeVisible();
await expect(locator).toBeHidden();

// Value
await expect(input).toHaveValue('John');

// Text content
await expect(element).toHaveText('Hello');
await expect(element).toContainText('Hell');

// Checked state
await expect(checkbox).toBeChecked();
await expect(checkbox).not.toBeChecked();

// Enabled/Disabled
await expect(button).toBeEnabled();
await expect(button).toBeDisabled();

// Count
await expect(locator).toHaveCount(5);

// URL
await expect(page).toHaveURL('https://example.com');

// Title
await expect(page).toHaveTitle('DNA Studio');
```

### Actions
Common interactions with elements:
```
// Click
await locator.click();
await locator.dblclick();
await locator.rightClick();

// Typing
await locator.fill('some text');       // clears and fills
await locator.type('some text');       // types character by character
await locator.clear();                 // clears field
await locator.press('Enter');          // keyboard key
await locator.pressSequentially('abc'); // types slowly

// Select dropdown
await select.selectOption({ label: 'Option A' });
await select.selectOption({ value: '1' });
await select.selectOption({ index: 2 });

// Checkbox / Radio
await checkbox.check();
await checkbox.uncheck();
await radio.click();

// Hover
await locator.hover();

// Focus
await locator.focus();

// Drag and drop
await locator.dragTo(targetLocator);

// Upload file
await locator.setInputFiles('path/to/file.pdf');

// Scroll
await locator.scrollIntoViewIfNeeded();
```

### Waits & Timeouts
Playwright has auto-waiting built in, but you can also wait explicitly:
```js
// Wait for element state
await locator.waitFor({ state: 'visible' });
await locator.waitFor({ state: 'hidden' });
await locator.waitFor({ state: 'attached' });

// Wait for navigation
await page.waitForURL('**/dashboard');
await page.waitForLoadState('networkidle');

// Wait for response
await page.waitForResponse('**/api/data');

// Custom timeout
await locator.click({ timeout: 10000 }); // 10 seconds
```
### Test Structure
```js
import { test, expect } from '@playwright/test';

// Group tests
test.describe('Login Feature', () => {

    // Run before each test
    test.beforeEach(async ({ page }) => {
        await page.goto('https://app.example.com');
    });

    // Run after each test
    test.afterEach(async ({ page }) => {
        await page.screenshot({ path: 'screenshot.png' });
    });

    // Individual test
    test('should login successfully', async ({ page }) => {
        await page.fill("//input[@name='email']", 'user@test.com');
        await page.fill("//input[@name='password']", 'password123');
        await page.click("//button[@type='submit']");
        await expect(page).toHaveURL('**/dashboard');
    });

    // Skip a test
    test.skip('skipped test', async ({ page }) => { });

    // Only run this test
    test.only('focused test', async ({ page }) => { });
});
```

### Fixtures
Reusable setup shared across tests:
```js
// fixtures.js
import { test as base } from '@playwright/test';
import { LoginPage } from './pages/LoginPage';
import { ProtocolHairPage } from './pages/ProtocolHairPage';

export const test = base.extend({
  loginPage: async ({ page }, use) => {
    await use(new LoginPage(page));
  },
  protocolPage: async ({ page }, use) => {
    await use(new ProtocolHairPage(page));
  },
});

// In your test file
import { test } from './fixtures';

test('fill protocol', async ({ protocolPage }) => {
  await protocolPage.fillProtocolHair({ ... });
});
```

### Configuration (playwright.config.js)
```js
import { defineConfig } from '@playwright/test';

export default defineConfig({
  testDir: './tests',
  timeout: 30000,
  retries: 2,
  reporter: 'html',

  use: {
    baseURL: 'https://app.dna-studio.com',
    headless: true,           // run without browser UI
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
    trace: 'on-first-retry',
  },

  projects: [
    { name: 'Chromium', use: { browserName: 'chromium' } },
    { name: 'Firefox',  use: { browserName: 'firefox' } },
    { name: 'WebKit',   use: { browserName: 'webkit' } },
  ],
});
```
### Data-Driven Testing
```js
// testData.json
{
  "protocol": {
    "description": "Hair test",
    "typeOfTest": "Mono-application",
    "substratum": "Volunteers"
  }
}

// In test
import testData from './testData.json';

test('data driven test', async ({ page }) => {
  const protocolPage = new ProtocolHairPage(page);
  await protocolPage.fillProtocolHair(testData.protocol);
});
```

### API Testing
Playwright can also test REST APIs:
```js
test('API test', async ({ request }) => {
  const response = await request.post('/api/studies', {
    data: { name: 'New Study', type: 'Sensory Expert' }
  });
  expect(response.status()).toBe(201);
  const body = await response.json();
  expect(body.name).toBe('New Study');
});
```

### Useful CLI Commands
```js
# Run all tests
npx playwright test

# Run specific file
npx playwright test protocol.spec.js

# Run in headed mode (see browser)
npx playwright test --headed

# Run specific browser
npx playwright test --project=chromium

# Debug mode (step through)
npx playwright test --debug

# Generate HTML report
npx playwright show-report

# Record new test (codegen)
npx playwright codegen https://app.example.com

# Update snapshots
npx playwright test --update-snapshots
```

### Recommended Folder Structure
```js
project/
├── pages/                        # Page Object Models
│   ├── GeneralInformationPage.js
│   ├── ProtocolHairPage.js
│   └── ...
├── tests/                        # Test files
│   ├── generalInformation.spec.js
│   ├── protocolHair.spec.js
│   └── ...
├── data/                         # Test data
│   └── testData.json
├── fixtures/                     # Shared fixtures
│   └── fixtures.js
├── playwright.config.js          # Configuration
└── package.json
```

