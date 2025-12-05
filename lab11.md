# API Testing Lab Instructions - Using GitHub Copilot

## Lab Overview
Learn how to create and test REST APIs using GitHub Copilot's AI-powered assistance. This hands-on lab will guide you through building API tests with Copilot's help.

## Prerequisites
- Visual Studio Code with GitHub Copilot extension
- Node.js (v18 or higher)
- Basic understanding of JavaScript/TypeScript
- GitHub Copilot subscription

---

## Lab Setup

### Step 1: Initialize Project

```bash
# Create project directory
mkdir api-testing-lab
cd api-testing-lab
npm init -y
```

### Step 2: Install Dependencies

```bash
npm install --save-dev @types/jest @types/node jest ts-jest typescript axios dotenv
npm install --save-dev @types/supertest supertest express
```

### Step 3: Configure TypeScript

Create `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "commonjs",
    "rootDir": "./src",
    "outDir": "./dist",
    "esModuleInterop": true,
    "strict": true,
    "skipLibCheck": true,
    "resolveJsonModule": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

### Step 4: Configure Jest

Create `jest.config.js`:

```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  roots: ['<rootDir>/src'],
  testMatch: ['**/__tests__/**/*.ts', '**/?(*.)+(spec|test).ts'],
  collectCoverageFrom: ['src/**/*.ts', '!src/**/*.d.ts'],
};
```

---

## Lab 1: Basic API Testing with Copilot

### Exercise 1.1: Create Test Helper

**Using Copilot Chat:**
1. Open Copilot Chat (`Ctrl+Shift+I`)
2. Type: `"Create an API client utility class for testing REST APIs with axios"`

Create `src/utils/api-client.ts`:

```typescript
import axios, { AxiosInstance, AxiosRequestConfig, AxiosResponse } from 'axios';

export class ApiClient {
  private client: AxiosInstance;

  constructor(baseURL: string) {
    this.client = axios.create({
      baseURL,
      timeout: 5000,
      headers: {
        'Content-Type': 'application/json',
      },
    });
  }

  async get<T>(url: string, config?: AxiosRequestConfig): Promise<AxiosResponse<T>> {
    return this.client.get<T>(url, config);
  }

  async post<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<AxiosResponse<T>> {
    return this.client.post<T>(url, data, config);
  }

  async put<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<AxiosResponse<T>> {
    return this.client.put<T>(url, data, config);
  }

  async delete<T>(url: string, config?: AxiosRequestConfig): Promise<AxiosResponse<T>> {
    return this.client.delete<T>(url, config);
  }

  setAuthToken(token: string) {
    this.client.defaults.headers.common['Authorization'] = `Bearer ${token}`;
  }
}
```

### Exercise 1.2: Write Your First API Test

**Using Copilot Inline Suggestions:**
1. Create a new file: `src/tests/basic-api.test.ts`
2. Start typing a comment and let Copilot suggest the test

```typescript
import { ApiClient } from '../utils/api-client';

describe('Basic API Tests', () => {
  let apiClient: ApiClient;

  beforeAll(() => {
    // Using JSONPlaceholder as a test API
    apiClient = new ApiClient('https://jsonplaceholder.typicode.com');
  });

  // Test GET request for fetching users
  test('GET /users should return list of users', async () => {
    const response = await apiClient.get('/users');
    
    expect(response.status).toBe(200);
    expect(Array.isArray(response.data)).toBe(true);
    expect(response.data.length).toBeGreaterThan(0);
  });

  // Test GET request for single user
  test('GET /users/1 should return a single user', async () => {
    const response = await apiClient.get('/users/1');
    
    expect(response.status).toBe(200);
    expect(response.data).toHaveProperty('id', 1);
    expect(response.data).toHaveProperty('name');
    expect(response.data).toHaveProperty('email');
  });

  // Test POST request
  test('POST /posts should create a new post', async () => {
    const newPost = {
      title: 'Test Post',
      body: 'This is a test post',
      userId: 1,
    };

    const response = await apiClient.post('/posts', newPost);
    
    expect(response.status).toBe(201);
    expect(response.data).toHaveProperty('id');
    expect(response.data.title).toBe(newPost.title);
  });
});
```

---

## Lab 2: Advanced Testing with Copilot

### Exercise 2.1: Authentication Testing

**Copilot Prompt:** `"Generate authentication tests with bearer token"`

Create `src/tests/authentication.test.ts`:

```typescript
import { ApiClient } from '../utils/api-client';

describe('Authentication Tests', () => {
  let apiClient: ApiClient;
  const mockToken = 'mock-jwt-token-12345';

  beforeAll(() => {
    apiClient = new ApiClient('https://jsonplaceholder.typicode.com');
  });

  test('should set authorization header with token', async () => {
    apiClient.setAuthToken(mockToken);
    
    try {
      const response = await apiClient.get('/posts/1');
      expect(response.config.headers?.Authorization).toBe(`Bearer ${mockToken}`);
    } catch (error) {
      // Expected for mock API
    }
  });

  test('should handle unauthorized access (401)', async () => {
    const unauthorizedClient = new ApiClient('https://httpstat.us');
    
    try {
      await unauthorizedClient.get('/401');
    } catch (error: any) {
      expect(error.response.status).toBe(401);
    }
  });
});
```

### Exercise 2.2: Data Validation Tests

**Use Copilot Chat:** `"Create tests to validate API response schema"`

Create `src/tests/data-validation.test.ts`:

```typescript
import { ApiClient } from '../utils/api-client';

interface User {
  id: number;
  name: string;
  username: string;
  email: string;
  address: {
    street: string;
    city: string;
    zipcode: string;
  };
}

describe('Data Validation Tests', () => {
  let apiClient: ApiClient;

  beforeAll(() => {
    apiClient = new ApiClient('https://jsonplaceholder.typicode.com');
  });

  test('should validate user object structure', async () => {
    const response = await apiClient.get<User>('/users/1');
    const user = response.data;

    // Validate required fields
    expect(user).toHaveProperty('id');
    expect(user).toHaveProperty('name');
    expect(user).toHaveProperty('email');
    expect(user).toHaveProperty('address');

    // Validate data types
    expect(typeof user.id).toBe('number');
    expect(typeof user.name).toBe('string');
    expect(typeof user.email).toBe('string');

    // Validate email format
    expect(user.email).toMatch(/^[^\s@]+@[^\s@]+\.[^\s@]+$/);
  });

  test('should validate array response', async () => {
    const response = await apiClient.get<User[]>('/users');
    
    expect(Array.isArray(response.data)).toBe(true);
    
    response.data.forEach(user => {
      expect(user).toHaveProperty('id');
      expect(user).toHaveProperty('name');
      expect(user).toHaveProperty('email');
    });
  });
});
```

---

## Lab 3: Using Copilot Chat for Complex Scenarios

### Exercise 3.1: Performance Testing

**In Copilot Chat, ask:**
```
"Create a performance test that measures API response time and handles concurrent requests"
```

Create `src/tests/performance.test.ts`:

```typescript
import { ApiClient } from '../utils/api-client';

describe('Performance Tests', () => {
  let apiClient: ApiClient;

  beforeAll(() => {
    apiClient = new ApiClient('https://jsonplaceholder.typicode.com');
  });

  test('API response time should be under 2 seconds', async () => {
    const startTime = Date.now();
    await apiClient.get('/users');
    const endTime = Date.now();
    
    const responseTime = endTime - startTime;
    expect(responseTime).toBeLessThan(2000);
  });

  test('should handle concurrent requests', async () => {
    const requests = Array(5).fill(null).map((_, index) => 
      apiClient.get(`/users/${index + 1}`)
    );

    const responses = await Promise.all(requests);
    
    responses.forEach(response => {
      expect(response.status).toBe(200);
    });
  });
});
```

### Exercise 3.2: Error Handling

**Ask Copilot:** `"Generate comprehensive error handling tests"`

Create `src/tests/error-handling.test.ts`:

```typescript
import { ApiClient } from '../utils/api-client';

describe('Error Handling Tests', () => {
  let apiClient: ApiClient;

  beforeAll(() => {
    apiClient = new ApiClient('https://jsonplaceholder.typicode.com');
  });

  test('should handle 404 Not Found', async () => {
    try {
      await apiClient.get('/users/999999');
      fail('Should have thrown an error');
    } catch (error: any) {
      expect(error.response.status).toBe(404);
    }
  });

  test('should handle network timeout', async () => {
    const slowApi = new ApiClient('https://httpstat.us');
    
    try {
      await slowApi.get('/200?sleep=6000');
    } catch (error: any) {
      expect(error.code).toBe('ECONNABORTED');
    }
  }, 10000);
});
```

---

## Lab 4: Copilot Best Practices

### Tips for Effective Copilot Usage:

#### 1. Use Clear Comments
```typescript
// Test GET endpoint that returns user profile with nested address object
```

#### 2. Leverage Copilot Chat Commands
- `/explain` - Understand existing code
- `/fix` - Fix errors in your tests
- `/tests` - Generate tests for your code
- `/doc` - Generate documentation

#### 3. Use @workspace for Context
```
@workspace How do I add authentication to my API tests?
```

#### 4. Iterate with Copilot
- **Accept** suggestions with `Tab`
- **Reject** with `Esc`
- **See alternatives** with `Alt+]` or `Alt+[`

#### 5. Inline Chat
- Press `Ctrl+I` to open inline chat
- Type your request directly in the editor
- Great for quick refactoring or modifications

---

## Lab 5: Running Your Tests

### Update package.json

Add test scripts to your `package.json`:

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "test:verbose": "jest --verbose"
  }
}
```

### Run Tests

```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Watch mode (re-runs on file changes)
npm run test:watch

# Run specific test file
npm test basic-api.test.ts

# Run tests matching a pattern
npm test -- --testNamePattern="GET /users"
```

### Expected Output

```
PASS  src/tests/basic-api.test.ts
  Basic API Tests
    ✓ GET /users should return list of users (234ms)
    ✓ GET /users/1 should return a single user (145ms)
    ✓ POST /posts should create a new post (189ms)

Test Suites: 1 passed, 1 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        2.456s
```

---

## Lab 6: Advanced Copilot Features

### Exercise 6.1: Generate Tests from Existing Code

1. Select your API client code
2. Right-click and choose **Copilot > Generate Tests**
3. Review and refine the generated tests

### Exercise 6.2: Fix Failing Tests

1. When a test fails, select the test code
2. Use **Copilot Chat**: `/fix why is this test failing?`
3. Apply suggested fixes

### Exercise 6.3: Improve Test Coverage

**In Copilot Chat:**
```
@workspace Analyze my test coverage and suggest additional test cases
```

---

## Common API Testing Scenarios

### Testing with Environment Variables

Create `.env.example`:

```env
API_BASE_URL=https://api.example.com
API_KEY=your-api-key-here
TIMEOUT=5000
```

Create `src/config/test-config.ts`:

```typescript
import dotenv from 'dotenv';

dotenv.config();

export const config = {
  apiBaseUrl: process.env.API_BASE_URL || 'https://jsonplaceholder.typicode.com',
  apiKey: process.env.API_KEY || '',
  timeout: parseInt(process.env.TIMEOUT || '5000', 10),
};
```

### Testing with Mock Data

Create `src/utils/test-helpers.ts`:

```typescript
export const mockUser = {
  id: 1,
  name: 'John Doe',
  email: 'john.doe@example.com',
  username: 'johndoe',
};

export const mockPost = {
  id: 1,
  title: 'Test Post',
  body: 'This is a test post body',
  userId: 1,
};

export function delay(ms: number): Promise<void> {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

---

## Troubleshooting Guide

### Common Issues and Solutions

#### Issue: Tests timing out
**Solution:**
```typescript
// Increase timeout for specific test
test('slow API call', async () => {
  // test code
}, 10000); // 10 second timeout
```

#### Issue: CORS errors
**Solution:**
```typescript
// Add CORS handling to your API client
this.client.defaults.headers.common['Access-Control-Allow-Origin'] = '*';
```

#### Issue: Authentication failures
**Ask Copilot:**
```
@workspace /explain why is authentication failing in my API tests?
```

---

## Project Structure

```
api-testing-lab/
├── src/
│   ├── tests/
│   │   ├── basic-api.test.ts
│   │   ├── authentication.test.ts
│   │   ├── data-validation.test.ts
│   │   ├── performance.test.ts
│   │   └── error-handling.test.ts
│   ├── utils/
│   │   ├── api-client.ts
│   │   └── test-helpers.ts
│   └── config/
│       └── test-config.ts
├── .env.example
├── .gitignore
├── jest.config.js
├── package.json
├── tsconfig.json
└── README.md
```

---


## Next Steps

### Intermediate Level:
1. **API Mocking**: Use tools like `nock` or `msw` with Copilot
2. **Contract Testing**: Implement Pact or similar frameworks
3. **CI/CD Integration**: Add tests to GitHub Actions workflow
4. **Database Testing**: Test APIs with database interactions

### Advanced Level:
1. **Load Testing**: Use k6 or Artillery
2. **Security Testing**: Test for vulnerabilities
3. **GraphQL Testing**: Extend to GraphQL APIs
4. **E2E Testing**: Combine with Playwright or Cypress

---

## Conclusion

Congratulations! You've completed the API Testing Lab with GitHub Copilot. You now have the skills to:

