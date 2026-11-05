# UI Lab Results

Tool parts that I chose: **Part 3: Robot Framework** and **Part 4: Cypress**

---

## Part 0

- **Step 0.1, Chrome version:**
  `157.0.8103.39`

- **Step 0.3, ChromeDriver version:**
  `157.0.8103.38`

- **Step 0.4, locator of Pizza, Please!:**
  `name=pizza-please`

- **Step 0.4, locator of Excluded tools:**
  `css=select`

- **Step 0.4, locator of Must be vegetarian:**
  `id=default-checkbox`

- **Step 0.4, locator of Custom Pizza Name:**
  `css=input#pizza-name`

- **Step 0.5, pizza name, tool and calories of the run by hand:**
  - Pizza name: `Lab Pizza 20261105-090900`
  - Tool: `Scissors`
  - Calories per slice: `550`

### QP-01 Manual Run

| Step | Actual result | Pass or fail |
|------|---------------|--------------|
| 1 | QuickPizza home page opened and heading showed `Looking to break out of your pizza routine?` |Pass |
| 2 | Advanced was enabled and the advanced fields appeared | Pass |
| 3 | Max calories = 600, Knife excluded, vegetarian checked, pizza name entered | Pass |
| 4 | Recommendation showed pizza name, tool = Scissors, calories per slice = 550 | Pass |
| 5 | After clicking Love it!, page showed `Please log in first.` | Pass |
| 6 | Logged in to `/admin` with admin/admin and `Latest pizza recommendations` appeared | Pass |
| 7 | Admin list showed pizza `Lab Pizza 20261105-090900` with tool `Scissors` | Pass |

---

## Part 3: Robot Framework

- **robot --version:**
  `Robot Framework 7.5.1`

- **Step 3.2, failure message for the wrong title:**
  `Title should have been 'Web Form' but was 'Web form'`

- **Step 3.8, run 1:**
  - Result: `PASS (1 test, 1 passed, 0 failed)`
  - Elapsed time: `00:00:10.237`
  - Pizza name: `Lab Pizza 20261105-093519`

- **Step 3.8, run 2:**
  - Result: `PASS (1 test, 1 passed, 0 failed)`
  - Elapsed time: `00:00:09.259`
  - Pizza name: `Lab Pizza 20261105-093538`

---

## Part 4: Cypress

- **node --version:**
  `v24.16.0`

- **npm --version:**
  `11.13.0`

- **npx cypress version:**
  `16.2.1`

- **Step 4.3, failure message for the wrong title:**
  `Timed out retrying after 10000ms.`
  `Expected 'Web Form' but the page title was 'Web form'.`

- **Step 4.6, tool and calories in the answer of POST /api/pizza:**
  - Tool: `Pizza cutter`
  - Calories: `500`

- **Step 4.7, the line of the admin list that shows your pizza:**
  `Lab Pizza 20261105-100516 (tool=Pizza cutter, ingredients_number=5)`

- **Step 4.8, run 1:**
  - Result: `PASS (2 tests, 2 passed, 0 failed)`
  - Duration: `00:16`
  - Pizza name: `Lab Pizza 20261105-101048`

- **Step 4.8, run 2:**
  - Result: `PASS (2 tests, 2 passed, 0 failed)`
  - Duration: `00:20`
  - Pizza name: `Lab Pizza 20261105-101311`

- **Step 4.9 (optional), browser and result:**
  - Browser: `Microsoft Edge`
  - Result: `PASS, both specs passed`

---

## Part B: Reflection

### 1. Max Calories per Slice locator

Why do the tests locate **Max Calories per Slice** through its label instead of its id?
What change to the page would allow the test to use an id, and why would that help a tester?

**Answer:**

The tests locate Max Calories per Slice through its label because several number inputs share the same id, so the id cannot uniquely identify the correct field. The page could be improved by giving this field a unique id such as max-calories. This would make the locator shorter, clearer, and easier to maintain.

---

### 2. Test oracle in QP-01 Step 7

Step 7 compares the tool in the admin list with the tool shown in the recommendation.
Identify the kind of test oracle and describe one QuickPizza fault that this check could catch.

**Answer:**

Step 7 uses a consistency oracle because it compares the tool in the admin list with the tool shown in the recommendation. In my Cypress run, the admin list showed Pizza cutter, which matched the tool from the recommendation. This check could catch a fault where the customer page and admin page show different tools for the same pizza.

---

### 3. Checking that the pizza is vegetarian

QP-01 does not currently check whether the recommended pizza is vegetarian.
Propose a check and explain what information the test would need from the page or another source.

**Answer:**

QP-01 could also check that the recommended pizza is vegetarian. In Cypress, the test could check that response.body.vegetarian from POST /api/pizza is true. The test needs this value from the page or another reliable source because the pizza name alone cannot prove that it is vegetarian.

---

### 4. Compare Robot Framework and Cypress

Compare the two tools you used. Include:

- How Robot Framework waited for QuickPizza
- How Cypress waited for QuickPizza
- How quickly you could write QP-01 using each tool
- How readable the Robot report/log was
- How readable the Cypress report/video was

**Answer:**

Robot Framework uses explicit waits such as Wait Until Element Is Visible, while Cypress automatically retries commands and assertions. My Robot runs took about 10.237 and 9.259 seconds, while the Cypress full runs took 16 and 20 seconds and included both specs. Robot logs were easy to follow by keyword, while Cypress screenshots and videos made the browser behavior easy to review.

---

### 5. Tool choice for Project 2

Choose either **Robot Framework** or **Cypress** for the automated UI tests in Project 2.
Give at least two reasons based on your experience in this lab.

**Answer:**

I would choose Cypress for the automated UI tests in Project 2 because:

Cypress automatically waits and retries commands, so I needed less explicit waiting code than in Robot Framework. It also supports cy.intercept() and automatically creates useful screenshots and videos for test evidence.

---

### 6. Robot Framework

If QuickPizza changes the locator of the **Max Calories per Slice** field, explain where you would change the locator and how the resource file keeps that change out of the test file.

**Answer:**

If the Max Calories locator changes, I would update ${MAX CALORIES} in robot/resources/quickpizza.resource. The locator is stored in the resource file instead of directly in pizza_scenario.robot. This means I can fix the locator in one place without changing the test scenario.

---

### 7. Cypress

Explain why QP-01 must stay as a **single test** in Cypress. Cypress clears cookies before each test. Explain what could go wrong if Steps 6 and 7 were moved into a second test.

**Answer:**

QP-01 must stay as one Cypress test because Cypress clears cookies before each test. QuickPizza uses a cookie to keep the browser connected to the same server, so splitting Steps 6 and 7 into another test could connect to a different server. The admin page might then not contain the pizza created in Steps 1-5, causing Step 7 to fail.