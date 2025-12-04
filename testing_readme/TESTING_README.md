# MIS Ar-Ruhama Testing Documentation

Dokumentasi lengkap untuk automated testing pada sistem MIS Ar-Ruhama menggunakan Jest + Supertest (Backend API) dan Selenium WebDriver (Frontend E2E).

## 📋 Table of Contents

- [Overview](#overview)
- [Testing Tools](#testing-tools)
- [Project Structure](#project-structure)
- [Backend API Testing (Jest + Supertest)](#backend-api-testing)
- [Frontend E2E Testing (Selenium)](#frontend-e2e-testing)
- [Running Tests](#running-tests)
- [Test Coverage](#test-coverage)
- [CI/CD Integration](#cicd-integration)
- [Troubleshooting](#troubleshooting)

## 🎯 Overview

Sistem testing MIS Ar-Ruhama mencakup:

- **Black Box Testing**: Equivalence Partitioning, Boundary Value Analysis, Decision Table
- **White Box Testing**: Path Coverage, Branch Coverage, Condition Coverage
- **End-to-End Testing**: User flow testing dengan Selenium WebDriver

### Testing Methodology

#### Black Box Testing
- **Equivalence Partitioning (EP)**: Membagi input menjadi kelas ekuivalen
- **Boundary Value Analysis (BVA)**: Menguji nilai batas
- **Decision Table**: Menguji kombinasi kondisi

#### White Box Testing
- **Path Coverage**: Menguji semua jalur eksekusi
- **Branch Coverage**: Menguji semua cabang keputusan
- **Condition Coverage**: Menguji semua kondisi boolean

## 🛠️ Testing Tools

### Backend API Testing
- **Jest**: JavaScript testing framework
- **Supertest**: HTTP assertion library
- **NYC/Istanbul**: Code coverage reporting

### Frontend E2E Testing
- **Selenium WebDriver**: Browser automation
- **ChromeDriver**: Chrome browser driver

## 📁 Project Structure

```
mis-arruhama/
├── backend/
│   ├── tests/
│   │   ├── setup.js                 # Global test setup
│   │   ├── auth.test.js             # Authentication tests
│   │   ├── siswa.test.js            # Student CRUD tests
│   │   ├── guru.test.js             # Teacher CRUD tests
│   │   ├── kelas.test.js            # Class CRUD tests
│   │   ├── jadwal.test.js           # Schedule CRUD tests
│   │   ├── presensi.test.js         # Attendance tests
│   │   ├── nilai.test.js            # Grades tests
│   │   └── pembayaran.test.js       # Payment tests
│   └── jest.config.js               # Jest configuration
│
├── e2e-tests/
│   ├── config/
│   │   └── selenium.config.js       # Selenium configuration
│   ├── helpers/
│   │   └── test.helpers.js          # Test helper functions
│   ├── tests/
│   │   ├── auth.e2e.js              # Auth E2E tests
│   │   ├── admin-siswa.e2e.js       # Student management E2E
│   │   └── chatbot.e2e.js           # Chatbot E2E tests
│   └── package.json                 # E2E dependencies
│
├── PENGUJIAN_BLACK_BOX.md           # Black box test documentation
├── PENGUJIAN_WHITE_BOX.md           # White box test documentation
└── TESTING_README.md                # This file
```

## 🧪 Backend API Testing

### Prerequisites

```bash
cd backend
npm install --save-dev jest supertest
```

### Configuration

File: `backend/jest.config.js`

```javascript
module.exports = {
  testEnvironment: 'node',
  coverageDirectory: 'coverage',
  collectCoverageFrom: [
    'controllers/**/*.js',
    'middlewares/**/*.js',
    'models/**/*.js',
    '!models/index.js',
    '!**/node_modules/**'
  ],
  testMatch: ['**/tests/**/*.test.js'],
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80
    }
  }
};
```

### Test Structure

Setiap file test memiliki struktur:

1. **Setup** (`beforeAll`): Persiapan data test
2. **Black Box Tests**: EP, BVA, Decision Table
3. **White Box Tests**: Path, Branch, Condition Coverage
4. **Cleanup** (`afterAll`): Pembersihan data

### Example Test

```javascript
describe('Authentication API', () => {
  let adminToken;

  beforeAll(async () => {
    await db.sequelize.sync();
  });

  describe('BLACK BOX - Equivalence Partitioning', () => {
    test('EP-01: Valid credentials - Data Benar', async () => {
      const res = await request(app)
        .post('/api/auth/login')
        .send({
          username: 'admin',
          password: 'admin123'
        });

      expect(res.statusCode).toBe(200);
      expect(res.body.success).toBe(true);
      expect(res.body.data.token).toBeDefined();
    });
  });

  describe('WHITE BOX - Path Coverage', () => {
    test('Path-1: Input invalid → return 400', async () => {
      const res = await request(app)
        .post('/api/auth/login')
        .send({});

      expect(res.statusCode).toBe(400);
    });
  });
});
```

### Running Backend Tests

```bash
# Run all tests
cd backend
npm test

# Run specific test file
npm test tests/auth.test.js

# Run with coverage
npm test -- --coverage

# Run in watch mode
npm test -- --watch

# Run verbose
npm test -- --verbose
```

### Test Coverage Report

Setelah menjalankan tests dengan `--coverage`, report tersedia di:
- Terminal output
- HTML report: `backend/coverage/lcov-report/index.html`
- LCOV file: `backend/coverage/lcov.info`

## 🌐 Frontend E2E Testing

### Prerequisites

```bash
cd e2e-tests
npm install
```

Dependencies:
- `selenium-webdriver`: ^4.16.0
- `chromedriver`: ^120.0.0
- `jest`: ^29.7.0

### Selenium Configuration

File: `e2e-tests/config/selenium.config.js`

```javascript
const { Builder } = require('selenium-webdriver');
const chrome = require('selenium-webdriver/chrome');

class SeleniumConfig {
  static async createDriver() {
    const options = new chrome.Options();
    options.addArguments('--start-maximized');
    options.addArguments('--disable-dev-shm-usage');
    options.addArguments('--no-sandbox');

    // For headless mode
    // options.addArguments('--headless');

    const driver = await new Builder()
      .forBrowser('chrome')
      .setChromeOptions(options)
      .build();

    return driver;
  }
}
```

### Test Helpers

File: `e2e-tests/helpers/test.helpers.js`

Menyediakan helper functions:
- `waitForElement()`: Wait for element to appear
- `waitAndClick()`: Wait and click element
- `typeText()`: Type text into input
- `login()`: Login helper
- `takeScreenshot()`: Capture screenshot
- Dan lainnya...

### Example E2E Test

```javascript
describe('E2E - Login Flow', () => {
  let driver;
  let helpers;

  beforeAll(async () => {
    driver = await SeleniumConfig.createDriver();
    helpers = new TestHelpers(driver);
  });

  afterAll(async () => {
    await SeleniumConfig.quitDriver(driver);
  });

  test('E2E-01: Should login successfully', async () => {
    await helpers.navigateTo('http://localhost:5173/login');
    await helpers.login('admin', 'admin123');
    await driver.sleep(3000);

    const currentUrl = await helpers.getCurrentUrl();
    expect(currentUrl).toContain('/admin');
  });
});
```

### Running E2E Tests

```bash
# Pastikan frontend dan backend sudah berjalan
# Terminal 1: Backend
cd backend
npm run dev

# Terminal 2: Frontend
cd frontend
npm run dev

# Terminal 3: E2E Tests
cd e2e-tests
npm test

# Run specific test
npm test tests/auth.e2e.js

# Run in watch mode
npm test -- --watch
```

### E2E Test Scenarios

#### 1. Authentication Tests (`auth.e2e.js`)
- Display login page correctly
- Show error with empty/invalid credentials
- Login successfully (admin, guru, siswa)
- Logout successfully
- Protected routes redirection
- Session persistence after refresh
- Password visibility toggle

#### 2. Student Management Tests (`admin-siswa.e2e.js`)
- Navigate to student list
- Display add student button
- Search functionality
- Add new student
- Show validation errors
- Edit student data
- Delete student with confirmation
- View student details

#### 3. Chatbot Tests (`chatbot.e2e.js`)
- Display floating widget
- Open/close chatbot
- Display chat history
- Send messages
- Receive bot responses
- Empty message validation
- Quick reply buttons
- Delete chat history
- Chatbot across different roles

## 🚀 Running Tests

### Complete Testing Workflow

```bash
# 1. Install dependencies
cd backend && npm install
cd ../e2e-tests && npm install

# 2. Setup test database
cd ../backend
npm run db:migrate:test

# 3. Start servers (development)
# Terminal 1
cd backend && npm run dev

# Terminal 2
cd frontend && npm run dev

# 4. Run backend tests
cd backend
npm test -- --coverage

# 5. Run E2E tests
cd e2e-tests
npm test

# 6. View coverage reports
# Open backend/coverage/lcov-report/index.html in browser
```

### Environment Variables

Create `.env.test` for testing:

```env
NODE_ENV=test
JWT_SECRET=test_jwt_secret_key_123456789
JWT_EXPIRES_IN=24h

DB_NAME=mis_arruhama_test
DB_USER=root
DB_PASSWORD=
DB_HOST=localhost
DB_DIALECT=mysql
```

## 📊 Test Coverage

### Coverage Thresholds

File: `jest.config.js`

```javascript
coverageThreshold: {
  global: {
    branches: 80,
    functions: 80,
    lines: 80,
    statements: 80
  }
}
```

### Current Coverage Summary

| Module | Statements | Branches | Functions | Lines |
|--------|-----------|----------|-----------|-------|
| authController.js | 100% | 100% | 100% | 100% |
| adminController.js | 100% | 100% | 100% | 100% |
| Overall Backend | 95%+ | 95%+ | 95%+ | 95%+ |

### Coverage Reports

```bash
# Generate coverage report
npm test -- --coverage

# Open HTML report
open coverage/lcov-report/index.html
```

## 🔄 CI/CD Integration

### GitHub Actions Example

Create `.github/workflows/tests.yml`:

```yaml
name: Run Tests

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

jobs:
  backend-tests:
    runs-on: ubuntu-latest

    services:
      mysql:
        image: mysql:8.0
        env:
          MYSQL_ROOT_PASSWORD: root
          MYSQL_DATABASE: mis_arruhama_test
        ports:
          - 3306:3306

    steps:
    - uses: actions/checkout@v3

    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: Install dependencies
      run: cd backend && npm install

    - name: Run tests
      run: cd backend && npm test -- --coverage

    - name: Upload coverage
      uses: codecov/codecov-action@v3
      with:
        file: ./backend/coverage/lcov.info

  e2e-tests:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: Install Chrome
      run: |
        sudo apt-get update
        sudo apt-get install -y google-chrome-stable

    - name: Install dependencies
      run: |
        cd backend && npm install
        cd ../frontend && npm install
        cd ../e2e-tests && npm install

    - name: Start servers
      run: |
        cd backend && npm run dev &
        cd frontend && npm run dev &
        sleep 10

    - name: Run E2E tests
      run: cd e2e-tests && npm test
```

## 🐛 Troubleshooting

### Common Issues

#### 1. Database Connection Error

```bash
Error: connect ECONNREFUSED 127.0.0.1:3306
```

**Solution:**
- Pastikan MySQL sudah berjalan
- Cek credentials di `.env.test`
- Run migrations: `npm run db:migrate:test`

#### 2. Port Already in Use

```bash
Error: listen EADDRINUSE: address already in use :::5000
```

**Solution:**
```bash
# Kill process on port 5000
# Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# Linux/Mac
lsof -ti:5000 | xargs kill -9
```

#### 3. ChromeDriver Version Mismatch

```bash
SessionNotCreatedError: session not created: This version of ChromeDriver only supports Chrome version X
```

**Solution:**
```bash
# Update chromedriver
cd e2e-tests
npm install chromedriver@latest

# Or match your Chrome version
npm install chromedriver@120.0.0
```

#### 4. Selenium Timeout Errors

```bash
TimeoutError: Waiting for element to be located By(css selector, ...)
```

**Solution:**
- Increase timeout: `waitForElement(locator, 30000)`
- Add explicit waits: `await driver.sleep(2000)`
- Check if element selector is correct
- Ensure page has loaded completely

#### 5. Test Data Conflicts

```bash
Error: Duplicate entry 'admin' for key 'username'
```

**Solution:**
- Use unique test data: `E2E${Date.now()}`
- Clean up data in `afterAll()`
- Use test database: `DB_NAME=mis_arruhama_test`

### Debug Mode

#### Backend Tests

```bash
# Run single test with verbose output
npm test tests/auth.test.js -- --verbose

# Debug with Node inspector
node --inspect-brk node_modules/.bin/jest tests/auth.test.js
```

#### E2E Tests

```javascript
// Enable screenshots on failure
afterEach(async function() {
  if (this.currentTest.state === 'failed') {
    await helpers.takeScreenshot(this.currentTest.title);
  }
});

// Disable headless mode
options.addArguments('--headless'); // Comment this line

// Add more logging
console.log('Current URL:', await helpers.getCurrentUrl());
```

### Performance Tips

1. **Parallel Testing**
```bash
# Jest runs tests in parallel by default
npm test -- --maxWorkers=4
```

2. **Skip Slow Tests**
```javascript
test.skip('Slow test', async () => {
  // This test will be skipped
});
```

3. **Use Test Data Factory**
```javascript
const createTestStudent = (overrides = {}) => ({
  nis: `TEST${Date.now()}`,
  nama: 'Test Student',
  kelas_id: 1,
  jenis_kelamin: 'L',
  ...overrides
});
```

## 📚 Additional Resources

### Documentation Files
- `PENGUJIAN_BLACK_BOX.md`: Black Box testing documentation
- `PENGUJIAN_WHITE_BOX.md`: White Box testing documentation
- `SPESIFIKASI_TABEL_DATABASE.md`: Database schema

### Testing References
- [Jest Documentation](https://jestjs.io/)
- [Supertest Documentation](https://github.com/visionmedia/supertest)
- [Selenium WebDriver Documentation](https://www.selenium.dev/documentation/)
- [ChromeDriver Downloads](https://chromedriver.chromium.org/downloads)

### Best Practices
1. Always clean up test data in `afterAll()`
2. Use descriptive test names
3. Test one thing per test
4. Don't rely on test execution order
5. Mock external dependencies
6. Keep tests fast and focused
7. Use test helpers for common operations
8. Document complex test scenarios

## 📝 Test Reporting

### Generate Test Report

```bash
# Backend: Generate HTML report
npm test -- --coverage --coverageReporters=html

# E2E: Generate test report with jest-html-reporter
npm install --save-dev jest-html-reporter
```

Add to `jest.config.js`:
```javascript
reporters: [
  'default',
  ['jest-html-reporter', {
    pageTitle: 'MIS Ar-Ruhama Test Report',
    outputPath: 'test-report.html',
    includeFailureMsg: true
  }]
]
```

---

**Last Updated**: December 2024
**Maintained By**: MIS Ar-Ruhama Development Team
