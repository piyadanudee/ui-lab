# UI lab results

Tool parts that I chose:
Part 3: Robot Framework
Part 4: Cypress

## Part 0

- Step 0.1, Chrome version: 122.0.6261.129
- Step 0.3, ChromeDriver version: 122.0.6261.128
- Step 0.4, locator of Pizza, Please!: button[name="pizza-please"]
- Step 0.4, locator of Excluded tools: select
- Step 0.4, locator of Must be vegetarian: input#default-checkbox
- Step 0.4, locator of Custom Pizza Name: input#pizza-name
- Step 0.5, pizza name, tool and calories of the run by hand:

| Step | Actual result | Pass or fail |
|------|---------------|--------------|
| 1 | Correct home page heading | PASS |
| 2 | Advanced fields appeared | PASS |
| 3 | All restrictions and pizza name were correct | PASS |
| 4 | Pizza cutter, 500 calories | PASS |
| 5 | Please log in first. | PASS |
| 6 | Admin login successful | PASS |
| 7 | Pizza name not found in admin list | FAIL |


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
  Node.js 22.14.0, npm 10.9.2, Cypress 16.2.1
- Step 4.3, failure message for the wrong title:
  Timed out retrying after 10000ms
  Expected 'Web Form' but the actual title was 'Web form'.
- Step 4.8, run 1, result, duration and pizza name:
  PASS, 00:17, pizza name not recoverable
- Step 4.8, run 2, result, duration and pizza name:
  PASS, 00:16, Lab Pizza 20261116-213958
