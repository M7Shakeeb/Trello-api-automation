# Trello API Automation Framework

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Trello](https://img.shields.io/badge/Trello-0052CC?style=for-the-badge&logo=trello&logoColor=white)
[![Trello API Automated Tests](https://github.com/M7Shakeeb/Trello-api-automation/actions/workflows/main.yml/badge.svg)](https://github.com/M7Shakeeb/Trello-api-automation/actions/workflows/main.yml)

## 📄 Project Overview
This repository contains a robust automated test suite for the **Trello REST API**. It does more than just happy-path testing, this framework is designed to handle **dynamic data**, **stateful workflows**, and **negative test scenarios**.

It simulates a realistic user journey: creating a board, managing lists, moving cards, and performing cleanup. These are all fully automated using Postman and JavaScript.

## 🧪 Key Automation Strategies
I made this collection while keeping in mind that I need to solve these common automation challenges:

### 1. 🛡️ Dynamic Data & Collision Prevention
* **Problem:** Hardcoding board names (e.g., "Test Board") causes tests to fail if the board already exists from a previous run.
* **Solution:** Implemented a JavaScript creation script using `Math.floor(Math.random())` to generate unique board names (e.g., `Trello Board 849`) for every single execution.

### 2. 🔗 Intelligent Request Chaining
* **Problem:** APIs return different IDs every time a resource is created.
* **Solution:** The framework captures dynamic IDs (`boardId`, `listId`, `cardId`) from JSON responses and stores them as **Collection Variables**. These variables are automatically passed to subsequent requests, creating a seamless E2E workflow.

### 3. 🔐 Security Best Practices
* **Problem:** Hardcoding API Keys in test files leads to security leaks.
* **Solution:** All authentication credentials (`trelloKey`, `trelloToken`) are extracted into **Postman Environments**, ensuring sensitive keys are never committed to version control.

---

## 🤖 CI/CD Pipeline (GitHub Actions)
This project is not just a local script; it is integrated into a **Continuous Integration** pipeline.
* **Tool:** [Newman](https://www.npmjs.com/package/newman) (Postman CLI).
* **Trigger:** Runs automatically on every `push` to the main branch.
* **Security:** API keys are injected at runtime via **GitHub Secrets**, ensuring no sensitive data is exposed in the repo.
* **Status:** You can see the live build status via the "passing" badge at the top of this README.

---

## ⚙️ The "User Journey" (Test Scenario)
The automation script simulates a real user performing a complete project lifecycle:

1.  **Project Initiation (POST Create Board):**
    * *The "Why":* Simulates a user starting a new project. We capture the specific `boardId` to ensure subsequent tests only interact with *this* board, not existing ones.
2.  **Validation (GET Board):**
    * *The "Why":* Verifies the board was actually created on the server and that default permission levels (Private) are correct.
3.  **Workflow Setup (POST Lists):**
    * *The "Why":* WE now introduce lists into this board. We create "To-Do" and "Done" columns to prepare for task management.
4.  **Task Creation (POST Card):**
    * *The "Why":* Simulates a user adding a task ("Sign Up for Trello") to the "To-Do" column.
5.  **Task Completion (PUT Card):**
    * *The "Why":* Simulating a business logic, we move the card to the "Done" list and assert that its `idList` property has actually updated.
6.  **Cleanup (DELETE Board):**
    * *The "Why":* Self-cleaning automation. We delete the specific board we created to prevent cluttering the environment (State Management).

---

## 🚀 How to Run Locally

### Prerequisites
* [Postman](https://www.postman.com/downloads/) installed.
* A Trello Account (to generate API Key & Token).

### Installation Steps
1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/M7Shakeeb/Trello-api-automation.git](https://github.com/M7Shakeeb/Trello-api-automation.git)
    ```
2.  **Import to Postman**
    * Open Postman.
    * Click **Import** -> Upload `Trello API.postman_collection.json`.
3.  **Setup Environment**
    * Create a new Environment in Postman named `Trello - Dev`.
    * Add variable: `trelloKey` (Your Trello API Key).
    * Add variable: `trelloToken` (Your Trello Token).
    * Add variable: `BaseURL` -> `https://api.trello.com/1/`.
4.  **Run Tests**
    * Select the collection and click **Run**.
    * Watch the tests execute sequentially!

---

## 📂 Project Structure
```text
trello-api-automation/
├── .github/workflows/main.yml    # The CI/CD Pipeline Configuration
├── Trello API.postman_collection.json  # The Main Test Script
└── README.md                     # Documentation

## 👨‍💻 Author
**Shakeeb Mohammed**
* QA & Test Automation Engineer
