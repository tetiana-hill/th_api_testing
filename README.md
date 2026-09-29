# API & Backend QA Portfolio

Practical API testing portfolio by **Tetiana Hil**, QA Engineer with a backend-focused testing background.

This repository demonstrates how I approach REST API testing: requirements analysis, risk-based test design, positive and negative scenarios, authentication, response validation, pagination/search/sorting, state-changing operations, and clear documentation of test-environment limitations.

## System under test

The current portfolio stage uses **DummyJSON**, a public fake REST API intended for testing and prototyping.

Base URL: `https://dummyjson.com`

Covered areas:
- authentication and JWT token handling;
- products API;
- search, pagination and sorting;
- create/update/delete contract checks;
- negative and HTTP-status scenarios;
- Postman automated assertions.

> **Important environment limitation:** DummyJSON simulates product create/update/delete operations. Those mutations are returned by the API but are not persisted on the server. Persistence/database validation is therefore intentionally out of scope for this stage.

## Repository structure

```text
.
├── README.md
├── docs/
│   ├── test-strategy.md
│   └── test-cases.md
└── postman/
    ├── DummyJSON-QA-Portfolio.postman_collection.json
    └── DummyJSON-QA.postman_environment.json
```

## What this project demonstrates

- REST API functional testing
- API contract and response validation
- positive / negative testing
- JWT authentication flow
- environment and token variables
- boundary-oriented pagination checks
- search and sorting validation
- CRUD contract checks
- automated Postman assertions
- explicit separation of API behavior from persistence guarantees
- risk-based test documentation

## Quick start

1. Import both files from `postman/` into Postman.
2. Select the **DummyJSON QA** environment.
3. Run the collection in order.
4. The login request stores `accessToken` and `refreshToken` automatically.
5. Review Postman test results for each request.

The collection uses the public DummyJSON demo credentials documented by the API provider.

## Test documentation

- [Test strategy](docs/test-strategy.md)
- [Test cases](docs/test-cases.md)

## Roadmap

Next portfolio stages will add:
- Newman command-line execution;
- GitHub Actions CI;
- expanded negative and boundary coverage;
- JSON Schema validation;
- a separate backend test environment with a real database for API ↔ DB consistency checks;
- Python/Playwright and Java API automation projects as separate portfolio repositories.

## About me

I'm a QA Engineer with 6+ years of commercial experience, focused on backend, API, databases, microservices and distributed systems.

[LinkedIn — Tetiana Hil](https://www.linkedin.com/in/tetiana-hil)
