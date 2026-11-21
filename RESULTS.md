
# UI lab results

Tool parts that I chose:
- Part 1: Selenium IDE
- Part 4: Cypress

## Part 0

- Step 0.1, Chrome version: 157.0.8103.80
- Step 0.3, ChromeDriver version: 157.0.8103.80
- Step 0.4, locator of Pizza, Please!: `button[name="pizza-please"]`
- Step 0.4, locator of Excluded tools: `label[for="countries_multiple"] + select`
- Step 0.4, locator of Must be vegetarian: `input#default-checkbox`
- Step 0.4, locator of Custom Pizza Name: `input#pizza-name`
- Step 0.5, pizza name, tool and calories of the run by hand: Lab Pizza 20261121-144000, Pizza cutter, 450 calories per slice.

| Step | Actual result | Pass or fail |
|---|---|---|
| 1 | Opened QuickPizza. Heading displayed correctly. | PASS |
| 2 | Enabled Advanced. All required fields displayed. | PASS |
| 3 | Entered Max Calories=600, excluded Knife, checked vegetarian, and entered Lab Pizza 20261121-144000. | PASS |
| 4 | Generated Lab Pizza 20261121-144000. Tool=Pizza cutter, Calories per slice=450. | PASS |
| 5 | Clicked Love it! without login. Received Please log in first. | PASS |
| 6 | Logged in using admin/admin. Latest pizza recommendations displayed. | PASS |
| 7 | Found Lab Pizza 20261121-144000 in admin list. Tool=Pizza cutter, ingredients_number=8. | PASS |

## Part 1: Selenium IDE

- Step 1.5, target chosen for Submit: `xpath=//button[@type='submit']`
- Step 1.5, the original recorded target `css=.btn` was fragile because the class may be shared by multiple buttons.
- Step 1.5, the replacement target is more stable because it identifies the button by its type attribute.

## Part 4: Cypress

- Node.js: v24.14.1
- Cypress: 16.2.1
- Browser: Electron 146

### Test Run 1
- pizza-scenario.cy.js: Passed (1/1)
- web-form.cy.js: Passed (1/1)
- Total: 2 Passed, 0 Failed
- Duration: 14 seconds

### Test Run 2
- pizza-scenario.cy.js: Passed (1/1)
- web-form.cy.js: Passed (1/1)
- Total: 2 Passed, 0 Failed
- Duration: 14 seconds
- Pizza Name: Lab Pizza 20261122-011355
- Tool: Scissors
- Ingredients: 7

### Evidence

Screenshots:
- qp01-step4-recommendation.png
- qp01-step5-login-needed.png
- qp01-step7-admin-list.png

Videos:
- pizza-scenario.cy.js.mp4
- web-form.cy.js.mp4

## Part B: Reflection

### 1. Why do the tests locate Max Calories per Slice through its label instead of its id?

The tests locate Max Calories per Slice through its label because the page uses the same id, "floating_filled", for three different input fields. I tested this in Chrome DevTools using `$$('#floating_filled')` and found that the page contains three matching elements. Using the label "Max Calories per Slice" allows the test to identify the correct input through its associated label. The page could be improved by assigning a unique id such as "max-calories-per-slice" to the input. This would make the locator more direct, reliable, and easier to maintain.

### 2. What kind of test oracle is Step 7?

Step 7 uses a consistency test oracle because it compares the tool shown in the pizza recommendation with the tool stored in the admin list. In my manual test, the recommendation showed Pizza cutter, and the admin list also showed Pizza cutter. This check could catch a fault where QuickPizza displays one tool to the user but saves a different tool in the admin list. It helps verify that the generated recommendation and stored data are consistent.

### 3. How could QP-01 check that the pizza is vegetarian?

QP-01 could check the ingredients of the generated pizza and verify that every ingredient is vegetarian. The test could compare the ingredients against a predefined list of vegetarian and non-vegetarian ingredients. The page would need to expose the complete ingredient list, or the test could retrieve the recipe data from an API or database. This would provide stronger evidence than simply checking whether the Must be vegetarian checkbox is selected.

### 4. Compare the two tools that you used.

Selenium IDE waits for elements using explicit commands such as wait for element visible, where I can specify a target and a maximum waiting time of 10 seconds. Cypress automatically waits and retries commands and assertions until the expected condition is met or the timeout is reached. Selenium IDE was faster for the initial recording because it captured browser actions automatically, but I had to manually edit commands, add waits, and add assertions to complete QP-01. Cypress required writing JavaScript code, so it took more effort at the beginning, but its Command Log, screenshots, and videos made it easier to understand what happened during a test run.

### 5. Choose the tool that you would use for the automated UI tests of Project 2.

I would choose Cypress for the automated UI tests of Project 2. First, Cypress automatically waits for elements and retries assertions, which helps make tests more reliable when the page loads dynamically. Second, Cypress provides clear test results, screenshots, and videos that make debugging easier. It also does not require a separate ChromeDriver installation, which simplifies the testing environment.

### 6. Part 1: Selenium IDE

The recorder chose `css=.btn` for the Submit button. This target is fragile because the CSS class btn may be shared by multiple buttons on the page, so the test could click the wrong button if another button is added before Submit. I replaced it with `xpath=//button[@type='submit']`, which identifies the button through its type attribute. This target is more stable because it describes the function of the button rather than its appearance or position on the page.

### 7. Part 4: Cypress

QP-01 must be implemented as a single test because Cypress clears cookies before each test. QuickPizza uses a cookie to keep the browser connected to the same server, and the admin list only displays pizzas created on that server. If steps 6 and 7 were placed in a second test, the cookies would be cleared and the browser might connect to a different server. As a result, the admin list might not contain the pizza created in steps 1 to 5, causing the test to fail. Keeping all seven steps in one test preserves the same browser session and allows the admin page to find the pizza created earlier.

## Conclusion

All Cypress test cases passed successfully in both test runs. The Selenium IDE and Cypress test evidence has been committed and pushed to the GitHub repository.
