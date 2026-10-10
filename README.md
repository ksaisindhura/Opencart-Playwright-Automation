# Playwright + TypeScript Automation

A Playwright and TypeScript portfolio project with web UI tests against [AwesomeQA](https://awesomeqa.com/ui/) and REST API tests against [FakeStoreAPI](https://fakestoreapi.com/). These are separate demo targets; the UI and API tests do not represent one integrated application.

## Coverage

- **Web UI:** registration, login/logout, product search, cart flows, and admin-page scenarios.
- **REST API:** products, users, carts, authentication, CRUD workflows, and JSON schema validation.
- **Test design:** Page Object Model, reusable fixtures, data-driven tests using CSV/JSON/Excel, generated test data, and multiple reporters.
- **Automation:** GitHub Actions, Docker Compose, and a Jenkins pipeline configuration.

## Tech stack

- Playwright Test and TypeScript
- Node.js and npm
- AJV for JSON Schema validation
- Faker.js for generated test data
- CSV/JSON/Excel test-data readers
- Playwright HTML, JUnit XML, Allure, and custom HTML reporting

## Project structure

```text
api/
  endpoints/
  schemas/
fixtures/
pages/
testdata/
tests/
  api/
  web/
utils/
playwright.config.ts
package.json
.github/workflows/playwright.yml
Dockerfile
docker-compose.yml
Jenkinsfile
```

## Prerequisites

- Node.js 20 or later
- npm
- Git
- Java only if you want to generate or open Allure reports locally
- Docker Desktop only if you want to run the Docker setup

## Setup

Clone this repository:

```bash
git clone https://github.com/ksaisindhura/Opencart-Playwright-Automation.git
cd Opencart-Playwright-Automation
npm ci
npx playwright install chromium
```

Create your local environment file:

**PowerShell**
```powershell
Copy-Item .env.example .env
```

**macOS/Linux**
```bash
cp .env.example .env
```

Edit `.env` with test credentials for the UI demo site if you want to run tests that require a valid account. Do not commit `.env` or real credentials. The API tests use the public FakeStoreAPI demo service.

## Running tests

Run all configured tests:

```bash
npx playwright test
```

Run a test group by tag:

```bash
npm run test:api
npm run test:web
npm run test:sanity
npm run test:regression
npm run test:e2e
npm run test:datadriven
npm run test:master
```

Run with a visible browser:

```bash
npx playwright test --headed
```

The Playwright configuration currently enables Chromium. Firefox and WebKit are not enabled in the configuration.

## Reports

The test configuration produces a Playwright HTML report, JUnit XML, Allure results, and a custom HTML report.

```bash
npx playwright show-report reports
npx allure generate allure-results --clean -o allure-report
npx allure open allure-report
```

Report folders and test artifacts are generated locally and are not intended to be committed.

## CI and containers

- **GitHub Actions:** runs on pushes and pull requests to `main`; you can also manually select a tagged suite from the Actions tab.
- **Docker Compose:** use `docker compose build` followed by `docker compose run --rm playwright-tests`.
- **Jenkins:** a pipeline definition is included in `Jenkinsfile`; configure the required Jenkins plugins and agent before using it.

## Notes

The web UI and API suites target different public demo services. Their behavior and availability can change independently, and tests that require a valid UI account need credentials configured in the local `.env` file.