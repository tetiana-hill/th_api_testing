# API Test Cases

| ID | Area | Scenario | Expected result | Priority |
|---|---|---|---|---|
| AUTH-01 | Auth | Login with valid demo credentials | 200; tokens and identity returned; response matches JSON Schema | High |
| AUTH-02 | Auth | Login with invalid password | 400; request rejected; no access token | High |
| AUTH-03 | Auth | Get current user with valid Bearer token | 200; authenticated user returned | High |
| AUTH-04 | Auth | Get current user with invalid Bearer token | 401/403; protected profile is not returned | High |
| PROD-01 | Products | Get product by valid ID | 200; required fields returned; response matches JSON Schema | High |
| PROD-02 | Products | Get nonexistent product | 404 | Medium |
| PROD-03 | Products | Pagination with limit=5 and skip=10 | 200; pagination metadata consistent; list matches JSON Schema | Medium |
| PROD-04 | Products | Pagination beyond dataset | 200; empty products array; requested skip preserved | Medium |
| PROD-05 | Products | Boundary limit=0 | 200; all items returned according to DummyJSON contract | Medium |
| PROD-06 | Products | Search using a value with no matches | 200; empty collection and total=0 | Medium |
| PROD-07 | Products | Search products for "phone" | 200; returned product text matches search term | Medium |
| PROD-08 | Products | Sort products by title ascending | 200; titles ordered ascending | Medium |
| PROD-09 | Products | Add product with valid JSON body | Successful response; submitted fields and generated ID returned | Medium |
| PROD-10 | Products | Patch product title | 200; updated title returned | Medium |
| PROD-11 | Products | Delete existing product | 200; deletion metadata returned | Medium |
| HTTP-01 | HTTP | Request explicit 404 mock endpoint | 404 returned | Low |

## Validation layers

The executable collection now combines:
- HTTP status validation;
- selected header/content-type checks;
- field-level assertions;
- **JSON Schema validation** for key authentication, single-product and product-list responses;
- business/data invariants;
- authentication negative testing;
- pagination boundary testing;
- no-result search behavior.

## Notes

### Mutation limitation

DummyJSON product create/update/delete operations are simulated. Mutation scenarios validate the HTTP/API contract only and do **not** claim durable-storage coverage.

### Dataset stability

Because this is a public test API, assertions avoid full static payload snapshots. Checks focus on stable contracts, types, requested parameters and response invariants.

### Why these boundary cases?

The added cases deliberately cover behavior at and beyond useful input boundaries: an offset beyond the available dataset, `limit=0`, a search with zero matches, and an invalid authentication token. These cases complement the happy-path checks without inventing requirements that the public API does not document.
