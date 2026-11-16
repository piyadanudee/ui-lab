# UI lab results

Tool parts that I chose:

- Part 3: Robot Framework
- Part 4: Cypress

## Part 0

- Step 0.1, Chrome version: 122.0.6261.129
- Step 0.3, ChromeDriver version: 122.0.6261.128
- Step 0.4, locator of Pizza, Please!: `button[name="pizza-please"]`
- Step 0.4, locator of Excluded tools: `select`
- Step 0.4, locator of Must be vegetarian: `input#default-checkbox`
- Step 0.4, locator of Custom Pizza Name: `input#pizza-name`
- Step 0.5, pizza name, tool and calories of the run by hand:
  Lab Pizza 20261116-180005, Pizza cutter, 500 calories per slice.

| Step | Actual result | Pass or fail |
|---|---|---|
| 1 | Correct home page heading appeared | PASS |
| 2 | Advanced fields appeared | PASS |
| 3 | All restrictions and pizza name were correct | PASS |
| 4 | Pizza cutter, 500 calories per slice | PASS |
| 5 | Please log in first. | PASS |
| 6 | Admin login successful | PASS |
| 7 | Pizza name was not found in the admin list | FAIL |

## Part 3: Robot Framework

- robot --version: Robot Framework 7.5.1 (Python 3.12.2 on win32)
- Step 3.2, failure message for the wrong title:
  Title should have been 'Web Form' but was 'Web form'.
- Step 3.8, run 1, result, elapsed time and pizza name:
  PASS, 00:00:13, Lab Pizza 20261116-203634
- Step 3.8, run 2, result, elapsed time and pizza name:
  PASS, 00:00:12, Lab Pizza 20261116-203719

## Part 4: Cypress

- node --version, npm --version and npx cypress version:
  Node.js 22.14.0, npm 10.9.2, Cypress 16.2.1.
- Step 4.3, failure message for the wrong title:
  Timed out retrying after 10000ms.
  Expected 'Web Form' but the actual title was 'Web form'.
- Step 4.6, tool and calories in the answer of POST /api/pizza:
  Tool: Scissors, calories: 575.
- Step 4.7, the line of the admin list that shows your pizza:
  Lab Pizza 20261116-213958 (tool=Scissors, ingredients_number=8) (newest).
- Step 4.8, run 1, result, duration and pizza name:
  PASS, 00:17, pizza name not recoverable.
- Step 4.8, run 2, result, duration and pizza name:
  PASS, 00:16, Lab Pizza 20261116-213958.
- Step 4.9 (optional), browser and result:
  Not performed.

## Part B: Reflection

**1. Explain why the tests locate Max Calories per Slice through its label instead of its id. Propose a change to the page that would let a test use an id, and state why that change helps a tester.**

The tests locate the Max Calories per Slice input through its label because its id, `floating_filled`, is shared by three input fields on the page. Therefore, using this id alone would not uniquely identify the correct input. The page could be improved by assigning a unique id, such as `max-calories`, to the Max Calories per Slice input. This would allow testers to use a simple and reliable locator such as `#max-calories`. It would make the test easier to read and maintain.

**2. Step 7 of QP-01 compares the tool in the admin list with the tool in the recommendation. Identify the kind of test oracle that this check is, and describe one fault in QuickPizza that it would catch.**

This check is a consistency test oracle because it compares the tool displayed in two different parts of the application. The tool in the admin list should be the same as the tool in the pizza recommendation. For example, if QuickPizza displays Scissors in the recommendation but saves Knife in the admin list, the test will detect this inconsistency. This check helps ensure that the application stores and displays the correct pizza information.

**3. QP-01 never checks that the pizza is vegetarian. Propose a check that would, and state what the test would need from the page or from another source.**

I would add an assertion to check that the recommended pizza is vegetarian. The test could inspect the response from the POST `/api/pizza` request and verify that `response.body.vegetarian` is `true`. This would require the API response to provide a vegetarian field that indicates whether the recommended pizza meets the vegetarian requirement. The test could also inspect the ingredients to make sure that no meat or other non-vegetarian ingredients are included.

**4. Compare the two tools that you used. Describe how each one waited for QuickPizza, how quickly you could write QP-01 with it, and how readable its report, log or video was.**

Robot Framework uses explicit waiting keywords, such as `Wait Until Element Is Visible` and `Wait Until Page Contains`, to wait for elements and text to appear. Cypress automatically retries commands such as `cy.get()` and assertions until they pass or reach the configured timeout. I found Cypress convenient for writing QP-01 because its JavaScript syntax is concise and it supports checking API requests with `cy.intercept()`. Robot Framework provides readable keyword-based test steps and detailed HTML logs, while Cypress provides a clear test summary, screenshots, and video recordings. Both tools successfully completed the QP-01 test.

**5. Choose the tool that you would use for the automated UI tests of Project 2, and justify the choice with two reasons from this lab.**

I would choose Cypress for the automated UI tests in Project 2. First, Cypress automatically retries element queries and assertions, which helps tests wait for the application without using fixed delays. Second, its `cy.intercept()` feature allows tests to check API requests and compare server responses with the information displayed on the page. Cypress also provides screenshots and video recordings, which make it easier to review test results and investigate failures.

**6. Part 3: Robot Framework — Explain where you would change the locator of the calories box if QuickPizza changed it, and how the resource file keeps that change out of the test file.**

If QuickPizza changed the locator of the Max Calories per Slice input, I would update the `${MAX CALORIES}` variable in `quickpizza.resource`. The resource file stores the locator in one place and the keyword `Fill In The Pizza Request` uses that variable to interact with the input. Therefore, I would only need to update the locator in the resource file instead of changing the test case in `pizza_scenario.robot`. This makes the test easier to maintain and reduces duplicated locator information.

**7. Part 4: Cypress — Explain why QP-01 has to be a single test in Cypress, which clears the cookies before each test, and what would go wrong if steps 6 and 7 were a second test.**

QP-01 has to be a single test because Cypress clears cookies before each test. QuickPizza uses a cookie to keep the browser connected to the same server that handled the pizza request. If steps 6 and 7 were placed in a second test, Cypress would clear the cookie before the admin login test, and the browser might connect to a different server. As a result, the admin list might not contain the pizza created in the first test, causing the test to fail even though the pizza was created successfully.