# UI Testing Lab

ITDS362 - Software Quality Assurance and Testing

This repository contains my work for the Automated UI Testing lab.

## Tool Parts Chosen

- Part 3: Robot Framework
- Part 4: Cypress

## Robot Framework

The `robot` folder contains the Robot Framework tests for the Selenium web form and the QuickPizza QP-01 scenario. The `resources` folder contains reusable QuickPizza keywords and locators, while `results/run1` and `results/run2` contain evidence from two successful full runs.

Run the Robot Framework tests from the `robot` folder with:

```powershell
robot .
```

## Cypress

The `cypress` folder contains the Cypress end-to-end tests for the Selenium web form and the QuickPizza QP-01 scenario. The `cypress/screenshots` and `cypress/videos` folders contain screenshots and recordings from a successful full run.

Run all Cypress tests from the `cypress` folder with:

```powershell
npx cypress run --browser chrome
```