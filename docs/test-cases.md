# API Test Cases

| ID | Area | Scenario | Expected result | Priority |
|---|---|---|---|---|
| AUTH-01 | Auth | Login with valid demo credentials | 200; accessToken and refreshToken returned; user identity returned | High |
| AUTH-02 | Auth | Login with invalid password | 400; request is rejected; no usable access token returned | High |
| AUTH-03 | Auth | Get current user with valid Bearer token | 200; authenticated user object returned | High |
| PROD-01 | Products | Get product by valid ID | 200; requested product returned with required core fields | High |
| PROD-02 | Products | Get nonexistent product | 404; resource-not-found response returned | Medium |
| PROD-03 | Products | Get products with limit=5 and skip=10 | 200; max 5 products; skip=10; pagination metadata consistent | Medium |
| PROD-04 | Products | Search products for "phone" | 200; response collection returned; matching text validated for returned products | Medium |
| PROD-05 | Products | Sort products by title ascending | 200; titles are in ascending lexical order | Medium |
| PROD-06 | Products | Add product with valid JSON body | 201/200 per API contract; returned object contains submitted fields and generated ID | Medium |
| PROD-07 | Products | Patch product title | 200; returned object contains requested updated title | Medium |
| PROD-08 | Products | Delete existing product | 200; isDeleted=true and deletedOn returned | Medium |
| HTTP-01 | HTTP | Request explicit 404 mock endpoint | 404 returned | Low |

## Notes

### Mutation limitation

DummyJSON product create/update/delete operations are simulated. PROD-06/07/08 validate the HTTP/API contract only. They do **not** validate durable storage.

### Dataset stability

Because this is a public test API, assertions avoid relying on full static payload snapshots. The collection focuses on stable contract fields, types, requested parameters and response invariants.

### Future coverage

Planned additions include token refresh, malformed bodies, missing required/expected fields, additional pagination boundaries, schema validation, response-time observations, and CI execution.
