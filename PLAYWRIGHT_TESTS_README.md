# Invoice Automation Test Suite

Comprehensive Playwright test suite for the Invoice Automation System (`invoiceautomatesimulation.bricksandagent.com`)

## Overview

This test suite automates the Invoice Approval Workflow test case:
- **Test Case ID:** TC 001
- **Test Name:** Invoice Approval Workflow
- **Purpose:** Test the complete invoice approval workflow including authentication, duplicated invoice bucket navigation, and invoice approval

## Test Flow

```
1. Navigate to Sign-In Page
   ↓
2. Enter Email Address (gihanwpt@yopmail.com)
   ↓
3. Enter Password (Jrc@1234)
   ↓
4. Click Sign In Button
   ↓
5. Close Popup Window
   ↓
6. Click Duplicated Bucket (1008 invoices)
   ↓
7. Wait for Invoice Details Page to Load
   ↓
8. Click Approve Button
   ↓
9. Verify Invoice Approved (Buttons Disabled)
```

## Files Included

### Test Files
- **InvoiceAutomateTest.spec.js** - Main test file (JavaScript) - Recommended for running
- **InvoiceAutomateTest.spec.ts** - TypeScript version with full type definitions

### Configuration Files
- **playwright.config.ts** - Playwright configuration with reporter settings
- **package.json** - Project dependencies and npm scripts

### Documentation
- **TestSute.md** - Original test requirements
- **TestExecutionReport_Run3.html** - Previous successful test execution report
- **README.md** - This file

## Prerequisites

### System Requirements
- Node.js 18+ or later
- npm or yarn package manager
- Internet connection (to access the Invoice Automation System)
- Windows, macOS, or Linux

### Browser Support
- Chromium (Recommended)
- Firefox
- WebKit (Safari)

## Installation

### 1. Install Node.js
Download and install from https://nodejs.org/

### 2. Install Dependencies

```bash
npm install
```

This will install:
- `@playwright/test` - Playwright testing framework
- `@types/node` - TypeScript definitions for Node.js

## Running Tests

### Quick Start (Simplest)
```bash
npm test
```

### Run in Headed Mode (See Browser)
```bash
npm run test:headed
```

### Run in Debug Mode
```bash
npm run test:debug
```

### Run in UI Mode (Interactive)
```bash
npm run test:ui
```

### Run Specific Browser
```bash
npm run test:chrome     # Chromium only
npm run test:firefox    # Firefox only
npm run test:webkit     # WebKit only
```

### Run in Slow Mode (Debug - Single Worker)
```bash
npm run test:slow
```

### Generate Test Code (Codegen)
```bash
npm run codegen
```

### View Test Report
```bash
npm run report
```

## Test Execution Options

### Run with Specific Project
```bash
npx playwright test --project=chromium
```

### Run with Retries
```bash
npx playwright test --retries=3
```

### Run Specific Test
```bash
npx playwright test InvoiceAutomateTest
```

### Run with Verbose Output
```bash
npx playwright test --reporter=list
```

### Run with HTML Report
```bash
npx playwright test --reporter=html
```

## Test Variations Included

The test file includes **3 different test implementations**:

### 1. Full Test with Detailed Logging (Recommended)
```javascript
test('TC 001 - Invoice Approval Workflow', async ({ page }) => {
  // Comprehensive logging for debugging
  // Detailed step-by-step execution
  // Full verification results tracking
})
```

### 2. Simplified Test
```javascript
test('TC 001 - Invoice Approval Workflow (Simplified)', async ({ page }) => {
  // Streamlined execution
  // Minimal logging
  // Quick validation
})
```

### 3. Test with Retry Logic
```javascript
test('TC 001 - Invoice Approval Workflow (with Retry)', async ({ page }) => {
  // Automatic retry on failure
  // Handles transient failures
  // Robust error handling
})
```

## Expected Test Results

### Success Criteria
- ✓ All 9 steps execute successfully
- ✓ All 11+ verifications pass
- ✓ Invoice is approved (buttons transition to disabled)
- ✓ Test execution time < 15 seconds
- ✓ No errors or exceptions

### Sample Output
```
========================================
Starting Test Case: TC 001
========================================

--- Step 1: Navigate to Sign-In Page ---
✓ Step 1: Navigate to https://invoiceautomatesimulation.bricksandagent.com/sign-in
✓ Verification: Successfully navigated to sign-in page

--- Step 2: Enter Email Address ---
✓ Step 2: Enter email address: gihanwpt@yopmail.com
✓ Verification: Credentials entered correctly (Email: gihanwpt@yopmail.com)

...

========================================
Test Case Completed Successfully: PASSED
========================================

--- Test Summary ---
Test Case: TC 001
Status: PASSED
Total Steps: 9
Passed Verifications: 11
Failed Verifications: 0
Execution Time: 8.75 seconds
```

## Test Artifacts

After running tests, the following artifacts are generated:

### Reports
- **playwright-report/** - HTML test report (open with: `npm run report`)
- **test-results.json** - JSON format results
- **junit-results.xml** - JUnit format for CI/CD integration

### Screenshots & Videos
- **test-results/** - Directory containing:
  - Screenshots (only on failure)
  - Videos (on failure)
  - Trace files (debugging)

## Troubleshooting

### Issue: Tests Fail with "Element Not Found"
**Solution:** The page structure may have changed. Update selectors:
```bash
npm run codegen
```
Use the codegen tool to record updated interactions.

### Issue: "Sign in" Button Not Found
**Solution:** Wait for page to load:
```javascript
await page.waitForLoadState('networkidle');
await page.waitForTimeout(2000);
```

### Issue: Popup Not Closing
**Solution:** Different popup selectors:
```javascript
// Try these alternatives:
page.locator('button[aria-label="Close"]')
page.locator('mat-dialog-container button').first()
page.locator('[class*="close"]')
```

### Issue: "Network Unreachable"
**Solution:** 
- Check internet connection
- Verify URL is correct
- Check if website is accessible in browser
- Try with `--headed` flag to see actual browser

### Issue: "Timeout of 30000ms Exceeded"
**Solution:** Increase timeout:
```javascript
await page.goto(url, { timeout: 60000 });
```

## Authentication Details

### Test Credentials
- **Email:** gihanwpt@yopmail.com
- **Password:** Jrc@1234
- **Authentication Type:** OIDC (Identity Server Redirect)

### Note
The application uses OIDC authentication which may redirect to:
- `https://identitysimulation.bricksandagent.com` - Identity provider

The test handles this automatically.

## Configuration Details

### Test Configuration
```javascript
const TEST_CONFIG = {
  baseURL: 'https://invoiceautomatesimulation.bricksandagent.com',
  signInURL: '/sign-in',
  credentials: {
    email: 'gihanwpt@yopmail.com',
    password: 'Jrc@1234'
  },
  timeouts: {
    navigation: 30000,      // 30 seconds
    elementWait: 15000,     // 15 seconds
    actionDelay: 1000       // 1 second
  }
};
```

### Playwright Configuration
- **Retry on CI:** 2 retries
- **Workers:** Parallel execution (auto-detected)
- **Reporters:** HTML, JSON, JUnit, List
- **Screenshot:** Only on failure
- **Video:** Retained on failure
- **Trace:** On first retry

## CI/CD Integration

### GitHub Actions Example
```yaml
name: Invoice Automation Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm test
      - uses: actions/upload-artifact@v3
        if: always()
        with:
          name: playwright-report
          path: playwright-report/
```

## Advanced Usage

### Record New Test
```bash
npm run codegen
```
This opens Playwright Inspector to record interactions.

### Debug Specific Step
```bash
npx playwright test --debug
```
Opens interactive debugger. Use `step` command to navigate test.

### Run Tests in Parallel
```bash
npx playwright test --workers=4
```

### Run Tests Sequentially
```bash
npm run test:slow
```

### View Trace of Failed Test
```bash
npx playwright show-trace test-results/YOUR-TEST-NAME/trace.zip
```

## Performance Metrics

### Expected Execution Times
- **Full Test:** 8-12 seconds
- **Step 1-4 (Authentication):** 4-6 seconds
- **Step 5-6 (Navigation):** 2-3 seconds
- **Step 7-9 (Approval):** 2-3 seconds

### System Requirements for Testing
- **CPU:** 2+ cores
- **RAM:** 512 MB minimum
- **Disk Space:** 500 MB (includes browser cache)
- **Network:** 1+ Mbps

## Best Practices

1. **Use Full Test Version** for development and debugging
2. **Use Simplified Test** for quick validation
3. **Use Retry Version** for CI/CD pipelines
4. **Run in Headed Mode** for visual debugging
5. **Check Reports** after each test run
6. **Update Timeouts** based on environment speed

## Support & Documentation

- **Playwright Docs:** https://playwright.dev/
- **Locator Guide:** https://playwright.dev/docs/locators
- **Best Practices:** https://playwright.dev/docs/best-practices
- **Debugging:** https://playwright.dev/docs/debug

## License

MIT

## Version History

- **v1.0.0** - Initial test suite for Invoice Automation
  - TC 001 - Invoice Approval Workflow
  - 3 test variations
  - Full documentation
  - CI/CD ready

---

**Last Updated:** November 14, 2025
**Maintained By:** Test Automation Team