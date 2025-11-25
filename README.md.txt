# 🍌 Trello API Automation Framework

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Trello](https://img.shields.io/badge/Trello-0052CC?style=for-the-badge&logo=trello&logoColor=white)

## 📄 Project Overview
This repository contains a robust automated test suite for the **Trello REST API**. Unlike simple happy-path testing, this framework is designed to handle **dynamic data**, **stateful workflows**, and **negative test scenarios**.

It simulates a realistic user journey: creating a board, managing lists, moving cards, and performing cleanup—all fully automated via Postman and JavaScript.

## 🧪 Key Automation Strategies
I engineered this collection to solve common automation challenges:

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

## ⚙️ Workflow Covered
The automation script executes the following End-to-End (E2E) scenario:
1.  **POST:** Create a new Board (captures dynamic ID).
2.  **GET:** Verify Board details and default permissions.
3.  **POST:** Create "To-Do" and "Done" lists.
4.  **POST:** Create a Card on the "To-Do" list.
5.  **PUT:** Move the Card to the "Done" list (verifies business logic).
6.  **DELETE:** Remove the Board (Self-Cleaning logic).

---

## 🚀 How to Run Locally

### Prerequisites
* [Postman](https://www.postman.com/downloads/) installed.
* A Trello Account (to generate API Key & Token).

### Installation Steps
1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/YOUR-USERNAME/trello-api-automation.git](https://github.com/YOUR-USERNAME/trello-api-automation.git)
    ```
2.  **Import to Postman**
    * Open Postman.
    * Click **Import** -> Upload `TrelloV4 API.postman_collection.json`.
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
├── TrelloV4 API.postman_collection.json  # The Main Test Script
└── README.md                             # Documentation

## 👨‍💻 Author
**Shakeeb Mohammed**
* QA & Test Automation Engineer