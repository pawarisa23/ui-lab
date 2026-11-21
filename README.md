# ui-lab
Chrome version: 157.0.8103.80


# UI Automated Testing Lab

This repository contains my work for the ITDS362 Software Quality Assurance and Testing UI Lab.

## Selected Tools

### Part 1: Selenium IDE

The `selenium-ide/` folder contains the Selenium IDE project file (`ui-lab.side`) and the exported Java test file (`QP01customerTest.java`). Selenium IDE was used to record and automate browser interactions for the UI testing exercise.

**Run the test:**

```bash
npx selenium-side-runner -c "browserName=chrome" selenium-ide/ui-lab.side
```

### Part 4: Cypress

The `cypress/` folder contains the Cypress configuration, E2E test specifications, custom commands, screenshots, and test execution videos. It includes tests for the Selenium Web Form and the QuickPizza QP-01 scenario.

**Install dependencies:**

```bash
cd cypress
npm install
```

**Run all Cypress tests:**

```bash
npx cypress run --browser electron
```

## Test Evidence

Cypress test evidence is stored in:

- `cypress/cypress/screenshots/`
- `cypress/cypress/videos/`

Test results and reflections are documented in `RESULTS.md`.

## Repository

GitHub: https://github.com/pawarisa23/ui-lab
