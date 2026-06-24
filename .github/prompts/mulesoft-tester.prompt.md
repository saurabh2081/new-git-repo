---
title: "MuleSoft Test Scenario & Data Generator"
description: "Prompt to generate comprehensive test scenarios,  Postman collection, load-test plan, security checklist, and dummy test data for a MuleSoft API."
parameters:
  - name: api_spec
    type: file | paste
    description: "OpenAPI (preferred) or RAML, or endpoint+schema list"
  - name: test_types
    type: list
    default: [unit, integration, performance, sanity]
  - name: auth
    type: object
    description: "Authentication details if needed (type: OAuth2/Basic/APIKey)"
  - name: data_constraints
    type: object
    description: "Optional field constraints: maxLength, min, pattern, required fields"
  - name: output_formats
    type: list
    default: [Postman, test-data.json, docs.md, load-test]

---

Task:
- Read the provided api_spec or endpoint descriptions.
- For each endpoint/flow, generate:
  1. A short test summary (purpose, prerequisites).
  2. Test scenarios table covering: happy path, edge cases, negative tests, data-driven variants.
  3. Postman request tests with examples and environment variables for auth.
  4. Dummy test data files (JSON) with multiple records: valid, invalid, boundary.
  5. A minimal load-test scenario (k6 script) describing ramp-up and key metrics.
  6. A security checklist referencing OWASP API Top 10 relevant checks.
- Produce a README.md describing how to run each artifact locally (commands for Maven/Gradle for Newman for Postman, k6 for load tests).

Output:
- Zip-friendly structure suggestions, or separate files if requested.

Example user prompt:
"Generate full test suite for the Orders API. Attach openapi.yaml. Include unit and performance tests, and produce test-data.json with 50 records (25 valid, 25 invalid)."

Notes:
- When schema is missing, infer reasonable payloads from field names and common types.
- Flag ambiguous fields and suggest clarifying questions.
