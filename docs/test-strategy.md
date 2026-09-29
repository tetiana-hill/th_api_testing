# Test Strategy — DummyJSON API

## 1. Objective

Validate selected DummyJSON REST API behavior and demonstrate a structured backend/API QA approach using executable Postman checks and documented scenarios.

## 2. Scope

### In scope
- API availability / basic health
- authentication with valid and invalid credentials
- JWT access-token capture and authenticated user request
- product retrieval
- pagination
- search
- sorting
- simulated create, update and delete operations
- selected negative and HTTP-status behavior
- response status, body, headers, key field types and business-level assertions

### Out of scope
- UI testing
- load/performance testing
- security penetration testing
- database validation
- persistence of product mutations
- third-party integrations

## 3. Environment

Base URL: `https://dummyjson.com`

The SUT is a public fake REST API. Test data may be changed by the provider. Assertions should therefore prefer contracts and invariants over unnecessary hard-coded dataset values.

DummyJSON documents that product POST/PUT/PATCH/DELETE operations are simulated and are not persisted. This means the portfolio can validate request/response contracts for those operations, but must not claim database persistence coverage.

## 4. Test approach

### Functional
Validate expected behavior for documented endpoints and parameters.

### Negative
Check invalid authentication, nonexistent resources and explicit error/status endpoints.

### Contract
Validate HTTP status codes, JSON content type, required fields and important field types.

### Data consistency inside a response
Validate relationships such as:
- returned collection length does not exceed requested limit;
- `skip` reflects requested pagination offset;
- search results contain the search term in relevant product text;
- ascending sort returns titles in ascending order;
- created/updated responses echo requested values;
- delete response reports deletion metadata.

### Authentication flow
1. Login with documented demo credentials.
2. Capture access and refresh tokens.
3. Call authenticated-user endpoint with Bearer token.
4. Verify identity fields and token presence.

## 5. Risks and priorities

**High**
- authentication flow
- wrong status codes
- malformed/incorrect response contracts

**Medium**
- pagination/search/sorting logic
- CRUD response contracts

**Low**
- cosmetic response details not affecting API consumers

## 6. Entry criteria

- DummyJSON is reachable.
- Postman collection and environment are imported.
- Base URL is configured.

## 7. Exit criteria

- Critical and high-priority collection checks pass.
- Any unexpected behavior is documented with request, response, expected result and reproducible steps.
- Environment limitations are not reported as product defects.

## 8. Evidence

Executable checks live in `postman/DummyJSON-QA-Portfolio.postman_collection.json`.

Human-readable coverage is maintained in `docs/test-cases.md`.
