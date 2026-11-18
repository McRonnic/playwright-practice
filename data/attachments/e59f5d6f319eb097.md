# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: login_ddt.spec.ts >> factory test
- Location: tests\login_ddt.spec.ts:21:5

# Error details

```
Error: expect(received).toHaveProperty(path)

Expected path: "gggemail"
Received path: []

Received value: {"email": "test_1779655410972_7193@example.com", "password": "SecurePassword123!", "username": "user_1779655410972_7193"}
```

# Test source

```ts
  1  | import { test, expect } from '@playwright/test'
  2  | import LoginPage from '../pages/LoginPage.ts'
  3  | import { createRandomUser } from "../factories/userFactory.ts"
  4  | 
  5  | const credentials = [
  6  |     { username: 'locked_out_user', password: 'secret_sauce', expectedError: 'Epic sadface: Sorry, this user has been locked out.' },
  7  |     { username: 'standard_user', password: 'wrong_password', expectedError: 'Epic sadface: Username and password do not match any user in this service' },
  8  |     { username: '', password: 'secret_sauce', expectedError: 'Epic sadface: Username is required' }
  9  | ];
  10 | 
  11 | for (const attempt of credentials) {
  12 | 
  13 |     test(`Тест логина для пользователя: ${attempt.username}`, async ({ page }) => {
  14 |         const loginPage = new LoginPage(page);
  15 |         await loginPage.navigate();
  16 |         await loginPage.login(attempt.username, attempt.password)
  17 |         await expect(loginPage.errorButton).toContainText(attempt.expectedError);
  18 |     })
  19 | }
  20 | 
  21 | test("factory test", async () => {
  22 |     const newUser = createRandomUser()
  23 |     console.log(newUser)
> 24 |     await expect(newUser).toHaveProperty('gggemail');
     |                           ^ Error: expect(received).toHaveProperty(path)
  25 | } )
  26 | 
```