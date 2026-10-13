# REST API Testing Portfolio — Postman, Newman & GitHub Actions

[![API Tests](https://github.com/tetiana-hill/th_api_testing/actions/workflows/api-tests.yml/badge.svg)](https://github.com/tetiana-hill/th_api_testing/actions/workflows/api-tests.yml)

A practical REST API testing project demonstrating structured test design, automated API validation, and continuous integration.

The project covers authentication, product operations, positive and negative scenarios, API contract validation, and risk-based testing using Postman and Newman.

## System Under Test

**API:** [DummyJSON](https://dummyjson.com) — a public REST API designed for testing and prototyping.

**Base URL:** `https://dummyjson.com`

**Tested modules:**
- **Authentication** — login and authenticated user endpoints.
- **Products** — product retrieval, search, pagination, sorting, and simulated create/update/delete operations.
- **HTTP responses** — selected error and status-code endpoints.

**Environment limitation:** DummyJSON simulates product creation, updates, and deletion without persisting changes on the server. Therefore, database persistence and API-to-database consistency checks are outside the scope of this project.

## Tech Stack

| Tool | Purpose |
|---|---|
| Postman | API requests and automated test execution |
| JavaScript | Test scripts and response assertions |
| JSON Schema | Response structure and data type validation |
| Newman | Command-line execution of Postman collections |
| GitHub Actions | Automated CI test execution |

## Test Coverage

The project contains **16 documented API test scenarios** covering the following areas:

| Area | Test coverage |
|---|---|
| Authentication | Valid and invalid login, token capture, authenticated user access, invalid Bearer token |
| Products | Product retrieval, simulated creation, update, and deletion |
| Pagination | Limit and offset validation, empty pages, zero-limit boundary |
| Search | Matching and non-matching search queries |
| Sorting | Ascending product title order |
| API contracts | HTTP status codes, response fields, data types, JSON Schema |
| Negative testing | Invalid credentials, nonexistent resources, error responses |

Automated Postman assertions validate:
- HTTP response status codes
- Selected response headers
- Required response fields and data types
- JSON Schema compliance for key endpoints
- Authentication and user identity
- Pagination parameters and response consistency
- Search results and sorting order
- Simulated CRUD response contracts

Assertions prioritize stable API contracts and data invariants rather than relying on complete hard-coded response snapshots.

## Repository Structure

```text
.
├── README.md
├── docs/
│   ├── test-strategy.md
│   └── test-cases.md
├── postman/
│   ├── DummyJSON-QA-Portfolio.postman_collection.json
│   └── DummyJSON-QA.postman_environment.json
└── .github/
    └── workflows/
        └── api-tests.yml
```

- `docs/` — test strategy, scenarios, expected results, and priorities.
- `postman/` — executable API test collection and environment configuration.
- `.github/workflows/` — automated test execution through GitHub Actions.

## Getting Started

### Option 1 — Run Tests in Postman

1. Download or clone this repository.
2. Import the [Postman collection](postman/DummyJSON-QA-Portfolio.postman_collection.json).
3. Import the [Postman environment](postman/DummyJSON-QA.postman_environment.json).
4. Select the **DummyJSON QA** environment.
5. Open the Collection Runner and run the collection in its defined order.
6. Review the test results and assertions.

The successful login request automatically captures `accessToken` and `refreshToken` and stores them as environment variables for subsequent authenticated requests.

The environment uses publicly documented DummyJSON demo credentials.

### Option 2 — Run Tests with Newman

**Prerequisites:** Node.js and npm installed.

Install Newman:

```bash
npm install --global newman
```

Run the test collection from the repository root:

```bash
newman run postman/DummyJSON-QA-Portfolio.postman_collection.json \
  --environment postman/DummyJSON-QA.postman_environment.json
```

Newman displays the executed requests, assertion results, and any failures in the terminal.

## Test Documentation

- [Test Strategy](docs/test-strategy.md) — testing objectives, scope, approach, risks, priorities, and entry/exit criteria.
- [Test Cases](docs/test-cases.md) — documented test scenarios, expected results, and priorities.

The documentation is maintained separately from the executable collection to demonstrate both test design and implementation.

## Continuous Integration

API tests are integrated into a GitHub Actions CI pipeline using Newman.

The workflow is triggered by:
- Every push to the `main` branch
- Pull requests targeting `main`
- Manual execution using `workflow_dispatch`

The pipeline:
1. Checks out the repository.
2. Sets up Node.js.
3. Installs Newman.
4. Executes the Postman collection.
5. Reports test results and fails the job if assertions fail.

[View GitHub Actions test runs](https://github.com/tetiana-hill/th_api_testing/actions/workflows/api-tests.yml)

## Known Limitations and Observations

### Simulated CRUD Operations

DummyJSON does not persist product mutations.

Create, update, and delete scenarios validate API response contracts only. They do not verify database changes or durable storage.

### Invalid JWT Handling

During CI testing on September 29, 2026, DummyJSON returned `500 Internal Server Error` for certain invalid Bearer tokens.

The automated test verifies that invalid tokens do not grant authenticated access or expose protected user data.

The observed HTTP 500 response is documented as a known system anomaly, not as the expected behavior of a correctly implemented authentication API.

See [Known Observations](docs/test-cases.md#known-observations).

### Public Test Environment

DummyJSON is a publicly available demonstration API. Its test data and behavior may change.

Tests therefore focus on documented API contracts, field types, and response invariants to reduce unnecessary dependencies on static data.

## Future Improvements

Planned enhancements include:

- Expanded negative and boundary test coverage
- Additional authentication edge cases
- More comprehensive API contract validation
- A separate backend testing environment with a persistent database
- API-to-database consistency checks
- Database persistence and data integrity validation

## Related Projects

- [Python & Playwright Test Automation](https://github.com/tetiana-hill/th_playwright_python)

## About Me

I'm a QA Engineer with 6+ years of commercial software testing experience, including backend systems, APIs, databases, microservices, and distributed systems.

[LinkedIn — Tetiana Hil](https://www.linkedin.com/in/tetiana-hil)
