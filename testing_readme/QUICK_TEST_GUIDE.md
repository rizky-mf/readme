# Quick Test Guide - MIS Ar-Ruhama

Panduan cepat untuk menjalankan automated tests.

## 🚀 Quick Start

### 1. Install Dependencies

```bash
# Backend testing
cd backend
npm install

# E2E testing
cd ../e2e-tests
npm install
```

### 2. Run Backend API Tests (Jest + Supertest)

```bash
cd backend

# Run all tests
npm test

# Run with coverage
npm test -- --coverage

# Run specific test file
npm test tests/auth.test.js

# Run in watch mode
npm test -- --watch
```

### 3. Run E2E Tests (Selenium)

```bash
# Make sure backend and frontend are running first!

# Terminal 1: Start backend
cd backend
npm run dev

# Terminal 2: Start frontend
cd frontend
npm run dev

# Terminal 3: Run E2E tests
cd e2e-tests
npm test

# Run specific E2E test
npm test tests/auth.e2e.js
```

## 📊 Test Files Overview

### Backend API Tests (Jest + Supertest)

| File | Description | Test Cases |
|------|-------------|------------|
| [auth.test.js](backend/tests/auth.test.js) | Authentication API | 31 tests |
| [siswa.test.js](backend/tests/siswa.test.js) | Student CRUD | 45+ tests |
| [guru.test.js](backend/tests/guru.test.js) | Teacher CRUD | 40+ tests |
| [kelas.test.js](backend/tests/kelas.test.js) | Class CRUD | 35+ tests |
| [jadwal.test.js](backend/tests/jadwal.test.js) | Schedule CRUD | 40+ tests |
| [presensi.test.js](backend/tests/presensi.test.js) | Attendance | 30+ tests |
| [nilai.test.js](backend/tests/nilai.test.js) | Grades | 35+ tests |
| [pembayaran.test.js](backend/tests/pembayaran.test.js) | Payment | 35+ tests |

**Total**: 290+ test cases

### Frontend E2E Tests (Selenium)

| File | Description | Test Scenarios |
|------|-------------|----------------|
| [auth.e2e.js](e2e-tests/tests/auth.e2e.js) | Login/Logout flows | 11 scenarios |
| [admin-siswa.e2e.js](e2e-tests/tests/admin-siswa.e2e.js) | Student management | 11 scenarios |
| [chatbot.e2e.js](e2e-tests/tests/chatbot.e2e.js) | Chatbot functionality | 12 scenarios |

**Total**: 34 E2E scenarios

## 📋 Test Coverage

### Testing Methods Implemented

#### Black Box Testing
- ✅ Equivalence Partitioning (EP)
- ✅ Boundary Value Analysis (BVA)
- ✅ Decision Table Testing

#### White Box Testing
- ✅ Path Coverage
- ✅ Branch Coverage
- ✅ Condition Coverage

#### End-to-End Testing
- ✅ User Flow Testing
- ✅ Cross-browser Testing
- ✅ Integration Testing

## 🎯 Test Examples

### Example 1: Run Authentication Tests

```bash
cd backend
npm test tests/auth.test.js

# Output:
# PASS  tests/auth.test.js
#   Authentication API - White Box & Black Box Testing
#     BLACK BOX - Equivalence Partitioning
#       ✓ EP-01: Valid username and password (admin) - Data Benar (150ms)
#       ✓ EP-04: Empty username - Data Salah (45ms)
#       ...
#     WHITE BOX - Path Coverage
#       ✓ Path-1: Input invalid → return 400 (35ms)
#       ...
#
# Test Suites: 1 passed, 1 total
# Tests:       31 passed, 31 total
```

### Example 2: Run E2E Login Test

```bash
cd e2e-tests
npm test tests/auth.e2e.js

# Browser will open automatically and perform:
# 1. Navigate to login page
# 2. Enter credentials
# 3. Click login button
# 4. Verify redirect to dashboard
# 5. Test logout
```

### Example 3: View Coverage Report

```bash
cd backend
npm test -- --coverage

# Then open in browser:
# backend/coverage/lcov-report/index.html
```

## 🔧 Configuration Files

### Jest Configuration
- **File**: [backend/jest.config.js](backend/jest.config.js)
- **Coverage threshold**: 80%
- **Test timeout**: 30 seconds

### Selenium Configuration
- **File**: [e2e-tests/config/selenium.config.js](e2e-tests/config/selenium.config.js)
- **Browser**: Chrome
- **Base URL**: http://localhost:5173
- **Implicit wait**: 10 seconds

## 📖 Documentation

For detailed documentation, see:
- [TESTING_README.md](TESTING_README.md) - Complete testing guide
- [PENGUJIAN_BLACK_BOX.md](PENGUJIAN_BLACK_BOX.md) - Black Box test documentation
- [PENGUJIAN_WHITE_BOX.md](PENGUJIAN_WHITE_BOX.md) - White Box test documentation

## 🐛 Common Issues & Solutions

### Issue 1: Database Connection Error
```bash
Error: connect ECONNREFUSED 127.0.0.1:3306
```
**Solution**: Start MySQL service
```bash
# Windows
net start MySQL80

# Linux/Mac
sudo systemctl start mysql
```

### Issue 2: Port Already in Use
```bash
Error: listen EADDRINUSE: address already in use :::5000
```
**Solution**: Kill the process
```bash
# Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# Linux/Mac
lsof -ti:5000 | xargs kill -9
```

### Issue 3: ChromeDriver Not Found
```bash
Error: ChromeDriver could not be found
```
**Solution**: Install ChromeDriver
```bash
cd e2e-tests
npm install chromedriver
```

### Issue 4: Tests Timing Out
```bash
TimeoutError: Waiting for element
```
**Solution**: Increase timeout in test
```javascript
await helpers.waitForElement(locator, 30000); // 30 seconds
```

## ✅ Pre-Test Checklist

Before running tests, make sure:

- [ ] MySQL database is running
- [ ] Database is seeded with test data
- [ ] Environment variables are set (`.env.test`)
- [ ] Backend server is running (for E2E tests)
- [ ] Frontend server is running (for E2E tests)
- [ ] Chrome browser is installed (for E2E tests)
- [ ] All dependencies are installed

## 📊 Test Results Summary

After running all tests, you should see:

```
Backend API Tests:
✓ 290+ test cases passed
✓ Coverage: >95% (statements, branches, functions, lines)

Frontend E2E Tests:
✓ 34 scenarios passed
✓ All user flows working correctly

Total Test Execution Time: ~5-10 minutes
```

## 🎉 Success Indicators

Tests are successful when:

1. **All test suites pass** ✅
2. **Coverage thresholds met** (>80%) ✅
3. **No errors in console** ✅
4. **E2E tests complete without timeouts** ✅
5. **Screenshots captured (if enabled)** 📸

## 📞 Support

If you encounter issues:

1. Check [TESTING_README.md](TESTING_README.md) troubleshooting section
2. Review test logs and error messages
3. Check database connections and server status
4. Verify Chrome and ChromeDriver versions match
5. Contact development team

---

**Quick Commands Reference**:

```bash
# Install all dependencies
cd backend && npm install && cd ../e2e-tests && npm install

# Run all backend tests with coverage
cd backend && npm test -- --coverage

# Run all E2E tests (servers must be running!)
cd e2e-tests && npm test

# Run specific test file
npm test tests/auth.test.js

# Open coverage report
open backend/coverage/lcov-report/index.html
```

Happy Testing! 🚀
