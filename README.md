# e-CSDD System Test Automation Framework

A comprehensive test automation suite for the e-CSDD (Electronic Road Traffic Safety Directorate) system built with Playwright and TypeScript.

## 🚀 Features

- **Cross-browser testing** (Chromium, Firefox, WebKit)
- **Page Object Model** for maintainable test code
- **Comprehensive test coverage** with positive and negative scenarios
- **Detailed reporting** with screenshots and traces
- **CI/CD ready** configuration
- **Environment-specific** configurations
- **Parallel test execution**
- **Visual regression testing** capabilities

## 📋 Test Coverage

### Core Test Suites

#### 🔐 Authentication Tests
- Valid login scenarios
- Invalid credentials handling
- Session management
- Multi-factor authentication (if applicable)

#### 👤 User Profile Tests
- **Profile Verification**: Validate user profile information display
- **Profile Editing**: Test profile update functionality
- **Email Verification**: Confirm correct email display
- **Data Persistence**: Verify changes are saved correctly

#### 🚗 Vehicle Registry Tests
- **Advanced Search**: Multi-criteria vehicle search functionality
- **Filter Validation**: Test various filter combinations
- **Results Verification**: Validate search results accuracy
- **Detail Navigation**: Test vehicle detail page access
- **Pagination**: Test result pagination if applicable

#### ⚠️ Negative Test Cases
- **No Results Handling**: Test behavior with empty search results
- **Invalid Search Parameters**: Test system response to invalid inputs
- **Network Failure Scenarios**: Test offline/connection error handling
- **Rate Limiting**: Test system behavior under high load

### Test Scenarios Detail

#### Test 1: User Profile Verification
```typescript
Scenario: Verify user profile displays correct information
Given: User is logged into e-CSDD system
When: User navigates to profile page via avatar menu
Then: Profile page displays correct email address
And: All profile fields are properly populated
```

#### Test 2: Vehicle Registry Search
```typescript
Scenario: Perform filtered vehicle search
Given: User is logged into e-CSDD system
When: User navigates to Vehicle Registry
And: Applies filters (Brand: Citroen, Model: C3, Fuel: Petrol, Transmission: Manual, Price: 500-10,000)
Then: Search results match specified criteria
And: First result details page shows accurate information
```

#### Test 3: Edge Cases and Error Handling
```typescript
Scenario: Handle no search results gracefully
Given: User performs search with restrictive criteria
When: Search returns no results
Then: System displays appropriate "no results" message
And: User can modify search criteria easily
```

## 🛠️ Setup and Installation

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn package manager
- Git

### Quick Start
```bash
# Clone the repository
git clone <repository-url>
cd ecsdd-test-automation

# Install dependencies
npm install

# Install Playwright browsers
npx playwright install

# Run all tests
npm test

# Run tests in specific browser
npm run test:chrome
npm run test:firefox
npm run test:webkit

# Run tests in headed mode (with browser UI)
npm run test:headed

# Generate and view test report
npm run report
```

## 📁 Project Structure

```
ecsdd-test-automation/
├── tests/
│   ├── auth/
│   │   ├── login.spec.ts
│   │   └── logout.spec.ts
│   ├── profile/
│   │   ├── profile-verification.spec.ts
│   │   └── profile-editing.spec.ts
│   ├── vehicle-registry/
│   │   ├── vehicle-search.spec.ts
│   │   ├── vehicle-details.spec.ts
│   │   └── search-filters.spec.ts
│   └── negative-cases/
│       ├── no-results.spec.ts
│       └── error-handling.spec.ts
├── page-objects/
│   ├── BasePage.ts
│   ├── LoginPage.ts
│   ├── ProfilePage.ts
│   ├── VehicleRegistryPage.ts
│   └── VehicleDetailsPage.ts
├── utils/
│   ├── test-data.ts
│   ├── helpers.ts
│   └── constants.ts
├── config/
│   ├── playwright.config.ts
│   ├── test-environments.ts
│   └── test-users.ts
├── fixtures/
│   └── test-fixtures.ts
└── reports/
    ├── html-report/
    └── screenshots/
```

## ⚙️ Configuration

### Environment Variables
Create a `.env` file in the root directory:
```env
# Test Environment
BASE_URL=https://ecsdd.gov.lv
TEST_ENVIRONMENT=staging

# Test Users
TEST_EMAIL=test@example.com
TEST_PASSWORD=your_password

# Test Configuration
TIMEOUT=30000
RETRIES=2
PARALLEL_WORKERS=4
```

### Browser Configuration
The framework supports multiple browser configurations:
- **Chromium**: Desktop and mobile viewports
- **Firefox**: Cross-platform testing
- **WebKit**: Safari compatibility testing

## 🧪 Test Execution

### Running Specific Test Suites
```bash
# Run profile tests only
npm run test:profile

# Run vehicle registry tests
npm run test:vehicle-registry

# Run negative test cases
npm run test:negative

# Run tests with specific tag
npx playwright test --grep @smoke

# Run tests in debug mode
npx playwright test --debug
```

### Parallel Execution
Tests are configured to run in parallel by default:
```bash
# Run with custom worker count
npx playwright test --workers=6
```

## 📊 Reporting and Analysis

### Test Reports
- **HTML Report**: Comprehensive visual report with test results
- **JSON Report**: Machine-readable results for CI/CD integration
- **JUnit Report**: Compatible with most CI systems
- **Allure Report**: Advanced reporting with trends and analytics

### Screenshots and Videos
- Automatic screenshots on test failures
- Video recording for failed tests
- Visual comparison for UI regression testing

### Generating Reports
```bash
# Generate HTML report
npm run report

# Generate Allure report
npm run allure:generate
npm run allure:serve
```

## 🔄 CI/CD Integration

### GitHub Actions Example
```yaml
name: e-CSDD Test Suite
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npx playwright install --with-deps
      - run: npm test
      - uses: actions/upload-artifact@v3
        if: always()
        with:
          name: test-results
          path: test-results/
```

## 📝 Best Practices

### Test Organization
- **Group related tests** in logical suites
- **Use descriptive test names** that explain the scenario
- **Implement data-driven tests** for multiple input scenarios
- **Maintain test independence** - each test should be able to run standalone

### Page Object Model
- **Encapsulate page elements** and actions in page objects
- **Use explicit waits** instead of hard-coded delays
- **Implement reusable components** for common UI elements
- **Handle dynamic content** with proper wait strategies

### Maintenance
- **Regular dependency updates** to keep framework current
- **Review and refactor** test code periodically
- **Monitor test stability** and fix flaky tests promptly
- **Document test scenarios** and expected behaviors

## 🚨 Troubleshooting

### Common Issues
1. **Browser Launch Failures**: Ensure Playwright browsers are installed
2. **Element Not Found**: Check selectors and wait conditions
3. **Timeout Errors**: Increase timeout values for slow operations
4. **Flaky Tests**: Add proper wait conditions and retry logic

### Debug Mode
```bash
# Run specific test in debug mode
npx playwright test profile-verification.spec.ts --debug

# Use Playwright Inspector
npx playwright test --ui
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-test`)
3. Commit your changes (`git commit -am 'Add new test scenario'`)
4. Push to the branch (`git push origin feature/new-test`)
5. Create a Pull Request

### Code Standards
- Follow TypeScript best practices
- Use ESLint and Prettier for code formatting
- Write comprehensive test documentation
- Include appropriate error handling

## 📚 Additional Resources

- **Playwright Documentation**: https://playwright.dev/docs/intro
- **TypeScript Handbook**: https://www.typescriptlang.org/docs/
- **Testing Best Practices**: https://playwright.dev/docs/best-practices
- **Page Object Model Guide**: https://playwright.dev/docs/pom

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For questions or issues:
- Create an issue in the repository
- Check the troubleshooting section
- Review Playwright documentation
- Contact the QA team

---
