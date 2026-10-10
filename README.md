**# 🎭 Playwright + TypeScript Automation Framework**

\> **\*\*A production-grade, multi-layer test automation framework\*\*** for **\*\*Web UI\*\***, **\*\*REST API\*\***, and **\*\*Database\*\*** testing — built with Playwright, TypeScript, and the Page Object Model pattern.

[![Playwright]\(https\://img.shields.io/badge/Playwright-1.62.1-45ba4b?logo=playwright)]\(https\://playwright.dev)
[![TypeScript]\(https\://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript)]\(https\://www\.typescriptlang.org/)
[![Allure]\(https\://img.shields.io/badge/Allure-Reporting-orange)]\(https\://allurereport.com/)
[![Jenkins]\(https\://img.shields.io/badge/Jenkins-CI%2FCD-red?logo=jenkins)]\(https\://www\.jenkins.io/)
[![Docker]\(https\://img.shields.io/badge/Docker-Ready-2496ED?logo=docker)]\(https\://www\.docker.com/)
[![Node]\(https\://img.shields.io/badge/Node-20+-339933?logo=node.js)]\(https\://nodejs.org/)

\---

**## 📖 Table of Contents**

\- [Overview]\(#-overview)

\- [Key Features]\(#-key-features)

\- [Framework Architecture]\(#-framework-architecture)

\- [Project Structure]\(#-project-structure)

\- [Tech Stack]\(#-tech-stack)

\- [Prerequisites]\(#-prerequisites)

\- [Quick Start]\(#-quick-start)

\- [Environment Configuration]\(#-environment-configuration)

\- [Test Suites & Tags]\(#-test-suites--tags)

\- [Running Tests]\(#-running-tests)

\- [Page Object Model]\(#-page-object-model)

\- [API Testing]\(#-api-testing)

\- [Data-Driven Testing]\(#-data-driven-testing)

\- [Reporting]\(#-reporting)

\- [Docker Setup]\(#-docker-setup)

\- [CI/CD with Jenkins]\(#-cicd-with-jenkins)

\- [Utilities]\(#-utilities)

\- [Contributing]\(#-contributing)

\- [License]\(#-license)

\---

**## 🎯 Overview**

This project contains Playwright tests for two separate demo services: web UI tests on AwesomeQA and REST API tests against FakeStoreAPI. These are separate test targets, not one end-to-end flow.

\| Layer           | Technology                                  | What We Test                                                                       |

\| --------------- | ------------------------------------------- | ---------------------------------------------------------------------------------- |

\| 🌐 **\*\*Web UI\*\***   | Playwright + Page Object Model              | Customer registration, login/logout, product search, cart management, admin portal |

\| 🔌 **\*\*REST API\*\*** | Playwright \`request\` fixture + FakeStoreAPI | Products, users, carts, authentication, schema validation                          |

It is designed for **\*\*CI/CD integration\*\*** (Jenkins + Docker), supports **\*\*multiple reporting formats\*\***, and follows **\*\*industry best practices\*\*** for maintainability and readability.

\---

**## ✨ Key Features**

\- ✅ **\*\*Page Object Model (POM)\*\*** — 12 reusable page classes for clean test code

\- ✅ **\*\*Custom Test Fixtures\*\*** — Type-safe dependency injection for all page objects

\- ✅ **\*\*Multi-Layer Testing\*\*** — Web UI + REST API + Database in a single framework

\- ✅ **\*\*Tag-Based Test Suites\*\*** — \`@sanity\`, \`@regression\`, \`@api\`, \`@web\`, \`@e2e\`, \`@master\`, \`@datadriven\`

\- ✅ **\*\*Data-Driven Testing\*\*** — CSV, JSON, and Excel test data sources

\- ✅ **\*\*Random Test Data Generation\*\*** — Powered by Faker.js

\- ✅ **\*\*Schema Validation\*\*** — JSON Schema validation for API responses via AJV

\- ✅ **\*\*Accessibility Checks\*\*** — WCAG compliance testing via axe-core

\- ✅ **\*\*Multiple Reporters\*\*** — HTML, Allure, JUnit XML, Custom HTML dashboard

\- ✅ **\*\*Parallel Execution\*\*** — Fully parallel test execution with configurable workers

\- ✅ **\*\*CI/CD Ready\*\*** — Jenkins pipeline + Docker Compose support

\- ✅ **\*\*Retries & Artifacts\*\*** — Automatic retries, screenshots, videos, and traces on failure

\---

**## 🏗️ Framework Architecture**

\`\`\`mermaid

flowchart TB

    subgraph Config["⚙️ Configuration Layer"]

        direction LR

        PC["playwright.config.ts\<br/>Timeouts, reporters,\<br/>browsers, retries"]

        ENV[".env\<br/>URLs, credentials,\<br/>API keys"]

        TS["tsconfig.json\<br/>TypeScript compiler\<br/>options"]

    end

    subgraph Tests["🧪 Test Layer"]

        direction TB

        WEB["tests/web/\<br/>UI Tests\<br/>@web"]

        API["tests/api/\<br/>API Tests\<br/>@api"]

    end

    subgraph POM["📄 Page Object Layer"]

        HP["HomePage"]

        LP["LoginPage"]

        RP["RegisterPage"]

        CP["CartPage"]

        PP["ProductPage"]

        SP["SearchResultsPage"]

        AP["AdminLoginPage"]

        ACP["AdminCustomersPage"]

        ACEP["AdminCustomerEditPage"]

    end

    subgraph Utils["🔧 Utility Layer"]

        DG["dataGenerator.ts\<br/>Faker.js random data"]

        DR["DataReader.ts\<br/>CSV / JSON / Excel"]

        HLP["helper.ts\<br/>Price conversion,\<br/>test data helpers"]

        CR["CustomReporter.ts\<br/>Custom HTML dashboard"]

    end

    subgraph API_Layer["🌐 API Layer"]

        ROUTES["endpoints/routes.ts\<br/>All endpoint URLs"]

        SCHEMAS["schemas/\<br/>JSON Schemas for\<br/>response validation"]

    end

    subgraph Data["📁 Test Data"]

        CSV["opencart_logindata.csv"]

        JSON["opencart_logindata.json"]

        XLSX["opencart_logindata.xlsx"]

    end

    subgraph Reports["📊 Reporting Layer"]

        HTML["HTML Report\<br/>(reports/)"]

        ALLURE["Allure Report\<br/>(allure-results/)"]

        JUNIT["JUnit XML\<br/>(reports/)"]

        CUSTOM["Custom Dashboard\<br/>(custom-report/)"]

    end

    subgraph CI_CD["🚀 CI/CD Layer"]

        DOCKER["Docker /\<br/>Docker Compose"]

        JENKINS["Jenkins Pipeline"]

    end

    Tests --> POM

    Tests --> API_Layer

    Tests --> Utils

    Tests --> Data

    POM --> Fixtures["fixtures/pageFixtures.ts"]

    Fixtures --> Tests

    Tests --> Config

    Tests --> Reports

    CI_CD --> Config

    CI_CD --> Tests

\`\`\`

\---

**## 📁 Project Structure**

\`\`\`mermaid

graph TD

    ROOT["📦 playwright-opencart-ai/"] --> CONF["⚙️ Config Files"]

    ROOT --> SRC["📂 Source Code"]

    ROOT --> TEST["🧪 Tests"]

    ROOT --> DATA["📁 Test Data"]

    ROOT --> REPORTS["📊 Reports"]

    ROOT --> INFRA["🐳 Infrastructure"]

    CONF --> PC["playwright.config.ts"]

    CONF --> TS["tsconfig.json"]

    CONF --> PKG["package.json"]

    CONF --> ENV[".env.example"]

    CONF --> DI[".dockerignore"]

    CONF --> GI[".gitignore"]

    SRC --> PAGES["pages/\<br/>12 Page Objects"]

    SRC --> UTILS["utils/\<br/>5 Utilities"]

    SRC --> FIXTURES["fixtures/\<br/>pageFixtures.ts"]

    SRC --> API["api/\<br/>endpoints + schemas"]

    TEST --> WEB["tests/web/\<br/>8 UI test specs"]

    TEST --> API_T["tests/api/\<br/>8 API test specs"]

    DATA --> CSV["\*.csv"]

    DATA --> JSON["\*.json"]

    DATA --> XLSX["\*.xlsx"]

    REPORTS --> HTML["reports/"]

    REPORTS --> ALLURE["allure-results/"]

    REPORTS --> CUSTOM["custom-report/"]

    REPORTS --> TR["test-results/"]

    INFRA --> DOCKER["Dockerfile"]

    INFRA --> DC["docker-compose.yml"]

    INFRA --> ENTRY["docker-entrypoint.sh"]

    INFRA --> JENKINS["Jenkinsfile"]

    INFRA --> SETUP["env_setup.bat"]

\`\`\`

**### 📂 Folder Breakdown**

\| Path              | Purpose                                                                 |

\| ----------------- | ----------------------------------------------------------------------- |

\| \`pages/\`          | Page Object classes — each encapsulates locators + actions for a page   |

\| \`fixtures/\`       | Custom Playwright test fixtures for type-safe page object injection     |

\| \`tests/web/\`      | Web UI test specs (login, registration, cart, search, etc.)             |

\| \`tests/api/\`      | REST API test specs against FakeStoreAPI                                |

\| \`api/endpoints/\`  | Centralized API route definitions                                       |

\| \`api/schemas/\`    | JSON Schema files for API response validation                           |

\| \`utils/\`          | Shared utilities (data generation, readers, DB client, custom reporter) |

\| \`testdata/\`       | External test data files (CSV, JSON, Excel)                             |

\| \`reports/\`        | Generated HTML + JUnit reports                                          |

\| \`allure-results/\` | Allure-compatible test result files                                     |

\| \`custom-report/\`  | Custom HTML dashboard output                                            |

\| \`test-results/\`   | Playwright test artifacts (screenshots, videos, traces)                 |

\| \`docs/\`           | Additional documentation                                                |

\| \`prompts/\`        | AI prompt templates for test generation                                 |

\---

**## 🛠️ Tech Stack**

\| Technology                                                           | Version | Purpose                          |

\| -------------------------------------------------------------------- | ------- | -------------------------------- |

\| [Playwright]\(https\://playwright.dev/)                                | ^1.62.1 | Browser automation & API testing |

\| [TypeScript]\(https\://www\.typescriptlang.org/)                        | 5.x     | Type-safe test code              |

\| [Node.js]\(https\://nodejs.org/)                                       | 20+     | Runtime                          |

\| [Allure Playwright]\(https\://www\.npmjs.com/package/allure-playwright) | ^3.10.2 | Allure reporting integration     |

\| [Faker.js]\(https\://fakerjs.dev/)                                     | ^10.5.0 | Random test data generation      |

\| [AJV]\(https\://ajv.js.org/)                                           | ^8.20.0 | JSON Schema validation           |

\| [axe-core]\(https\://www\.npmjs.com/package/@axe-core/playwright)       | ^4.13.0 | Accessibility (WCAG) testing     |

\| [Luxon]\(https\://moment.github.io/luxon/)                             | ^3.7.2  | Date/time manipulation           |

\| [csv-parse]\(https\://www\.npmjs.com/package/csv-parse)                 | ^7.0.2  | CSV file parsing                 |

\| [xlsx]\(https\://www\.npmjs.com/package/xlsx)                           | ^0.18.5 | Excel file parsing               |

\| [dotenv]\(https\://www\.npmjs.com/package/dotenv)                       | ^17.4.2 | Environment variable management  |

\---

**## 📋 Prerequisites**

Before you begin, ensure you have the following installed:

\- **\*\*Node.js\*\*** v20 or later → [Download]\(https\://nodejs.org/)

\- **\*\*npm\*\*** v9+ (comes with Node.js)

\- **\*\*Git\*\*** → [Download]\(https\://git-scm.com/)

\- **\*\*Playwright browsers\*\*** (installed via setup script)

\- **\*\*Docker Desktop\*\*** (optional, for containerized execution) → [Download]\(https\://www\.docker.com/products/docker-desktop/)

\- **\*\*Java 11+\*\*** (optional, for Allure reporting) → [Download]\(https\://adoptium.net/)

\---

**## 🚀 Quick Start**

**### 1️⃣ Clone the Repository**

\`\`\`bash

git clone \<repository-url>

cd playwright-opencart-ai

\`\`\`

**### 2️⃣ Install Dependencies**

\`\`\`bash

npm install

\`\`\`

**### 3️⃣ Install Playwright Browsers**

\`\`\`bash

npx playwright install --with-deps

\`\`\`

**### 4️⃣ Configure Environment**

\`\`\`bash

cp .env.example .env

\`\`\`

Edit \`.env\` with your application URLs and credentials (see [Environment Configuration]\(#-environment-configuration)).

**### 5️⃣ Run All Tests**

\`\`\`bash

npx playwright test

\`\`\`

\---

**## 🔧 Environment Configuration**

The framework uses a \`.env\` file for all configurable settings. Copy \`.env.example\` to \`.env\` and update the values:

\`\`\`env

\# Environment

APP_ENV=qa                          # qa | prod | dev

\# Web Application

WEB_APP_URL=https\://awesomeqa.com/ui/

APP_EMAIL=your-email\@example.com

APP_PASSWORD=your-password

\# Product Details (for cart tests)

PRODUCT_NAME=MacBook

PRODUCT_QUANTITY=1

TOTAL_PRICE=$602.00

\# API (FakeStoreAPI)

API_BASE_URL=https\://fakestoreapi.com

USERNAME=mor_2314

PASSWORD=83r5^\_

USER_ID=1

PRODUCT_ID=1

CART_ID=1

LIMIT=3

START_DATE=2019-12-10

END_DATE=2020-10-10

\# Admin Portal

ADMIN_URL=http\://localhost/opencart/upload/admin/index.php

\`\`\`

\---

**## 🏷️ Test Suites & Tags**

Tests are organized using Playwright's tag system (\`@tag-name\` in test titles). Each tag maps to a reusable npm script:

\| Tag           | npm Script                | Description                                  |

\| ------------- | ------------------------- | -------------------------------------------- |

\| \`@master\`     | \`npm run test:master\`     | **\*\*Master suite\*\*** — all critical tests        |

\| \`@sanity\`     | \`npm run test:sanity\`     | **\*\*Sanity checks\*\*** — quick smoke tests        |

\| \`@regression\` | \`npm run test:regression\` | **\*\*Full regression\*\*** — comprehensive coverage |

\| \`@web\`        | \`npm run test:web\`        | **\*\*Web UI tests only\*\***                        |

\| \`@api\`        | \`npm run test:api\`        | **\*\*API tests only\*\***                           |

\| \`@e2e\`        | \`npm run test:e2e\`        | **\*\*End-to-end scenarios\*\***                     |

\| \`@datadriven\` | \`npm run test:datadriven\` | **\*\*Data-driven tests\*\***                        |

Tests can carry **\*\*multiple tags\*\*** for flexible execution:

\`\`\`typescript

test('Valid Login Flow @master @sanity @regression @web', async (...) => { ... });

test('GET - All Products @master @sanity @api', async (...) => { ... });

\`\`\`

\---

**## ▶️ Running Tests**

**### Run All Tests**

\`\`\`bash

npx playwright test

\`\`\`

**### Run by Tag (npm scripts)**

\`\`\`bash

npm run test:sanity          # Sanity tests only

npm run test:regression      # Regression tests

npm run test:web             # Web UI tests

npm run test:api             # API tests

npm run test:e2e             # End-to-end tests

npm run test:master          # Master suite

npm run test:datadriven      # Data-driven tests

\`\`\`

**### Run in Headed Mode (with browser visible)**

\`\`\`bash

npm run test:master:headed

\`\`\`

**### Run with Debugging**

\`\`\`bash

npm run test:sanity:debug    # Opens Playwright Inspector

\`\`\`

**### Run a Single Test File**

\`\`\`bash

npx playwright test tests/web/valid-login.spec.ts

\`\`\`

**### Run with Specific Project / Browser**

\`\`\`bash

npx playwright test --project=chromium

\`\`\`

**### Run with grep (custom tag filter)**

\`\`\`bash

npx playwright test --grep "@sanity"

npx playwright test --grep "@api|@web"    # Multiple tags

\`\`\`

**### Run in CI Mode (headless, 2 retries, 1 worker)**

\`\`\`bash

set CI=true && npx playwright test

\`\`\`

\---

**## 📄 Page Object Model**

The framework uses the **\*\*Page Object Model (POM)\*\*** pattern to separate test logic from page-specific implementation details.

**### How It Works**

Each web page gets its own **\*\*Page Object class\*\*** that encapsulates:

\- **\*\*Locators\*\*** — CSS selectors / Playwright getters for elements

\- **\*\*Actions\*\*** — Methods that perform operations (click, fill, select)

\- **\*\*Verifications\*\*** — Methods that check state (isVisible, getText)

**### Available Page Objects**

\| Class                   | File                             | Key Methods                                                          |

\| ----------------------- | -------------------------------- | -------------------------------------------------------------------- |

\| \`HomePage\`              | \`pages/HomePage.ts\`              | \`navigateTo()\`, \`searchProduct()\`, \`clickLogin()\`, \`clickRegister()\` |

\| \`LoginPage\`             | \`pages/LoginPage.ts\`             | \`login()\`, \`isLoginPageExists()\`, \`getWarningMessage()\`              |

\| \`RegisterPage\`          | \`pages/RegisterPage.ts\`          | \`completeRegistration()\`, \`isRegisterPageExists()\`                   |

\| \`MyAccountPage\`         | \`pages/MyAccountPage.ts\`         | \`isMyAccountPageExists()\`, \`isAuthenticated()\`, \`clickLogout()\`      |

\| \`SuccessPage\`           | \`pages/SuccessPage.ts\`           | \`isSuccessPageExists()\`, \`getSuccessHeadingText()\`                   |

\| \`LogoutPage\`            | \`pages/LogoutPage.ts\`            | \`isLogoutPageExists()\`, \`clickContinue()\`                            |

\| \`SearchResultsPage\`     | \`pages/SearchResultsPage.ts\`     | \`isProductDisplayed()\`, \`getSearchHeadingText()\`                     |

\| \`ProductPage\`           | \`pages/ProductPage.ts\`           | \`getProductName()\`, \`getProductPrice()\`, \`addToCart()\`               |

\| \`CartPage\`              | \`pages/CartPage.ts\`              | \`isCartPageExists()\`, \`isProductInCart()\`, \`getTotalPrice()\`         |

\| \`AdminLoginPage\`        | \`pages/AdminLoginPage.ts\`        | \`login()\`, \`isAdminLoginPageExists()\`                                |

\| \`AdminCustomersPage\`    | \`pages/AdminCustomersPage.ts\`    | \`dismissSecurityModal()\`, \`searchByEmail()\`, \`clickEditCustomer()\`   |

\| \`AdminCustomerEditPage\` | \`pages/AdminCustomerEditPage.ts\` | \`isEditCustomerPageExists()\`, \`getFirstNameValue()\`                  |

**## 🌐 API Testing**

The framework tests the [FakeStoreAPI]\(https\://fakestoreapi.com/) — a free REST API for e-commerce.

**### API Layer Structure**

\`\`\`

api/

├── endpoints/

│   └── routes.ts          # Centralized route definitions

└── schemas/

    ├── product_api_schema.json

    ├── user_api_schema.json

    └── cart_api_schema.json

\`\`\`

**### API Test Coverage**

\| Test File                       | Endpoints Covered                        |

\| ------------------------------- | ---------------------------------------- |

\| \`products.spec.ts\`              | GET all, GET by ID, CRUD operations      |

\| \`users.spec.ts\`                 | GET all, GET by ID, CRUD operations      |

\| \`carts.spec.ts\`                 | GET all, GET by ID, CRUD operations      |

\| \`auth.spec.ts\`                  | POST login authentication                |

\| \`schema-validation.spec.ts\`     | JSON Schema validation for all endpoints |

\| \`product-crud-workflow\.spec.ts\` | Full CRUD workflow for products          |

\| \`user-crud-workflow\.spec.ts\`    | Full CRUD workflow for users             |

\| \`cart-crud-workflow\.spec.ts\`    | Full CRUD workflow for carts             |

\---

**## 📊 Data-Driven Testing**

The framework supports **\*\*three external data formats\*\*** for data-driven tests:

\| Format    | Reader                     | File Example                       |

\| --------- | -------------------------- | ---------------------------------- |

\| **\*\*CSV\*\***   | \`DataProvider.readCsv()\`   | \`testdata/opencart_logindata.csv\`  |

\| **\*\*JSON\*\***  | \`DataProvider.readJson()\`  | \`testdata/opencart_logindata.json\` |

\| **\*\*Excel\*\*** | \`DataProvider.readExcel()\` | \`testdata/opencart_logindata.xlsx\` |

**## 📊 Reporting**

The framework generates **\*\*four types of reports\*\*** simultaneously:

\`\`\`mermaid

flowchart LR

    subgraph PW["Playwright Test Runner"]

        T1["Test 1"]

        T2["Test 2"]

        TN["Test N"]

    end

    PW --> R1["📄 HTML Report\<br/>(reports/index.html)"]

    PW --> R2["📊 Allure Report\<br/>(allure-results/)"]

    PW --> R3["📋 JUnit XML\<br/>(reports/results.xml)"]

    PW --> R4["🎨 Custom Dashboard\<br/>(custom-report/)"]

    R2 --> AR["allure generate →\<br/>allure-report/"]

    R4 --> CR["Open custom-report/\<br/>index.html in browser"]

\`\`\`

**### 1️⃣ Playwright HTML Report**

\`\`\`bash

\# Auto-generated after test run

open reports/index.html

\`\`\`

![Playwright HTML Report]\(images/Playwright%20HTML%20Report.png)

**### 2️⃣ Allure Report**

\`\`\`bash

\# Generate and serve Allure report

npx allure generate allure-results --clean -o allure-report

npx allure open allure-report

\`\`\`

![Allure Report]\(images/Allure%20Report.png)

**### 3️⃣ JUnit XML Report**

Generated at \`reports/results.xml\` — compatible with Jenkins CI integration.

**### 4️⃣ Custom HTML Dashboard**

A custom reporter (\`utils/CustomReporter.ts\`) generates a branded HTML dashboard with:

\- Test pass/fail/skip statistics

\- Step-by-step execution details

\- Screenshot attachments on failure

\- Console logs per test step

\- Video and trace links

\- Timeline and chart visualizations

Open \`custom-report/index.html\` in a browser to view.

![Custom HTML Dashboard]\(images/Custom%20HTML%20Dashboard.png)

\---

**## 🐳 Docker Setup**

Run tests in a **\*\*consistent, isolated container environment\*\*** — no local dependencies needed.

**### Build the Image**

\`\`\`bash

docker compose build

\`\`\`

**### Run Test Suites**

\`\`\`bash

\# Run all tests

docker compose run --rm playwright-tests

\# Run specific suites

docker compose run --rm playwright-tests sanity

docker compose run --rm playwright-tests regression

docker compose run --rm playwright-tests web

docker compose run --rm playwright-tests api

docker compose run --rm playwright-tests master

docker compose run --rm playwright-tests e2e

docker compose run --rm playwright-tests datadriven

\`\`\`

**### Pass Extra Playwright Arguments**

\`\`\`bash

docker compose run --rm playwright-tests web --headed --workers 2

\`\`\`

**### Key Docker Features**

\- **\*\*Layer caching\*\*** — \`package\*.json\` copied first, \`npm ci\` cached unless deps change

\- **\*\*Bind mounts\*\*** — Reports and artifacts persist on the host

\- **\*\*Container-only \`node_modules\`\*\*** — Not shadowed by host bind mount

\- **\*\*Entrypoint script\*\*** — Maps suite names to npm scripts automatically

\---

**## 🚇 CI/CD with Jenkins**
The project includes a **\*\*declarative Jenkins pipeline\*\*** (\`Jenkinsfile\`) for Windows build agents.

**### Pipeline Parameters**
\| Parameter    | Choices                                                                                                | Description             |

\| ------------ | ------------------------------------------------------------------------------------------------------ | ----------------------- |

\| \`TEST_SUITE\` | \`test:e2e\`, \`test:master\`, \`test:sanity\`, \`test:regression\`, \`test:api\`, \`test:web\`, \`test:datadriven\` | Which tests to run      |

\| \`BROWSER\`    | \`chromium\`, \`firefox\`, \`webkit\`                                                                        | Browser selection       |

\| \`MODE\`       | \`headless\`, \`headed\`                                                                                   | Headless or headed mode |

**### Post-Build Actions**

\- ✅ Archives HTML reports

\- ✅ Publishes JUnit XML results (test trend graph)

\- ✅ Generates and publishes Allure reports

\- ✅ Sends email notifications with status and report links

\- ✅ Cleans up \`allure-results\` on success

\---

**## 🔧 Utilities**

\| Utility          | File                      | Purpose                                                                 |

\| ---------------- | ------------------------- | ----------------------------------------------------------------------- |

\| \`RandomDataUtil\` | \`utils/dataGenerator.ts\`  | Generate random names, emails, passwords, addresses, dates via Faker.js |

\| \`DataProvider\`   | \`utils/DataReader.ts\`     | Read test data from CSV, JSON, and Excel files                          |

\| \`Helper\`         | \`utils/helper.ts\`         | Price string-to-number conversion, static test data helpers             |

\| \`CustomReporter\` | \`utils/CustomReporter.ts\` | Custom Playwright reporter generating a rich HTML dashboard             |

\---