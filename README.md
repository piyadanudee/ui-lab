# UI Lab — Automated UI Testing

## Selected Tool Parts

This repository contains the following two tool parts:

- **Part 3: Robot Framework**
- **Part 4: Cypress**

## Part 3: Robot Framework

The `robot/` folder contains Robot Framework automated UI tests using SeleniumLibrary. It includes tests for Selenium's Web Form and the QuickPizza QP-01 scenario, reusable keywords in `resources/quickpizza.resource`, and test evidence from two full runs in `results/run1/` and `results/run2/`.

**How to run the tests:**

Open a terminal in the `robot/` folder, activate the Python virtual environment, install the dependencies if necessary, and run:

```powershell
pip install -r requirements.txt
robot .
```

The ChromeDriver environment variable `CHROMEDRIVER` must point to the ChromeDriver executable.

## Part 4: Cypress

The `cypress/` folder contains Cypress end-to-end tests written in JavaScript. It includes the Web Form test, the QuickPizza QP-01 scenario, a custom admin login command, configuration files, screenshots, and video recordings from two full test runs.

**How to run the tests:**

Open a terminal in the `cypress/` folder, install the dependencies if necessary, and run:

```powershell
npm install
npx cypress run --browser chrome
```

## Test Evidence

- Robot Framework: HTML reports, logs, XML results, and screenshots are stored in `robot/results/`.
- Cypress: screenshots and video recordings are stored in `cypress/cypress/screenshots/` and `cypress/cypress/videos/`.

## Repository

GitHub: https://github.com/piyadanudee/ui-lab