# Flexible Web Test Automation Framework

## Overview

This is a flexible and modular web test automation framework designed to test the e-commerce website: [SauceDemo](https://www.saucedemo.com/v1/). The framework focuses on **clean separation of concerns** between:

- Test Logic (TestNG test classes)
- Page Object Model (POM)
- Web Test Automation Library (Selenium)

This design enables **future flexibility** where the Selenium WebDriver layer can be swapped out with other tools (e.g., Playwright, Cypress, etc.) **without modifying the POM or test classes**.

---

## Architecture

### 1. 🧪 `Test Classes` Package

- Contains all TestNG-based test classes
- Tests are **data-driven** using `@DataProvider`, Parallel execution is supported.
- These tests interact with POM classes only — keeping tests clean and focused on behavior and assertions.

---

### 2. 📦 `POM` Package

- Contains all Page Object Model (POM) classes representing the pages of the web application.
- Each class encapsulates:
  - Page-specific element locators
  - Page interactions
  - Navigation logic
- This separation allows you to write high-level business flows in tests **without directly using Selenium commands**.

---

### 3. 🛠️ `Actions` Package

The Actions package acts as a custom-built wrapper around Selenium WebDriver. This is where **all direct interactions with Selenium are centralized**, allowing the rest of the framework (Page Objects and Tests) to remain **completely decoupled** from Selenium APIs. This design makes it easy to switch to another automation library (like Playwright or Cypress) without touching your POMs or test cases.


 `SeleniumBrowserActions.java` & `SeleniumWebUIActions.java` classes isolate **Selenium-specific logic** from your test and POM layers.

- `SeleniumBrowserActions.java`: Manages browser setup and WebDriver lifecycle via `ThreadLocal` or `HashMap`.
- `SeleniumWebUIActions.java`: Provides high-level UI actions (click, sendText, etc.) with pre/post validations.

---

## Why This Architecture?

The key benefit of this structure is **decoupling your business logic (test scenarios and page interactions)** from the **underlying automation engine (Selenium)**.

If you ever decide to migrate to another automation tool (e.g., Playwright, Cypress), only the `SeleniumActions` layer will need to be replaced — leaving your POMs and tests **completely untouched**.

This ensures less code refactor, reusability and easier testing and maintenance.
