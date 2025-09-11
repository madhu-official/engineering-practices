# API style guide

Since software architecture centers around decoupled microservices that provide functionality via RESTful 
APIs with a JSON payload. Small engineering teams own, deploy and operate these microservices in their 
on-prem or cloud environments. Our APIs express most purely what our systems do, and are therefore highly 
valuable business assets.

It is ideal to adopt "API First" as a key engineering principle. Microservices development begins with API 
definition outside the code and ideally involves ample peer-review feedback to achieve high-quality APIs. 
API First encompasses a set of quality-related standards and fosters a peer review culture including a 
lightweight review procedure. We encourage teams to follow them to ensure that our APIs:

- are easy to understand and learn
- are general and abstracted from specific implementation and use cases
- are robust and easy to use
- have a common look and feel
- follow a consistent RESTful style and syntax
- are consistent with other teams’ APIs and our enterprise architecture standards


## API Principles

REST API is centered around business (data) entities exposed as resources that are identified via URIs and
can be manipulated via standardized CRUD-like methods using different representations, and hypermedia. 
RESTful APIs tend to be less use-case specific and come with less rigid client / server coupling and are 
more suitable for an ecosystem of (core) services providing a platform of APIs to build diverse new business
services.

- Prefer REST based APIs with JSON payload
- Prefer systems to be truly RESTFUL
- Be liberal in what you accept and conservative in what you send
- Follow resource based approach
- Should follow the `Richardson Maturity Model`



## API First Philosophy

API first should be considered the core part of the developer experience.

- define APIs first, before coding its implementation, using a standard specification language
- get early review feedback from peers and client developers
- profound understanding of the domain and required functionality
- generalized business entities / resources, i.e. avoidance of use case specific APIs
- clear separation of WHAT vs. HOW concerns, i.e. abstraction from implementation aspects — APIs should 
be stable even if we replace complete service implementation including its underlying technology stack
- single source of truth for the API specification; it is a crucial part of a contract between service provider and client users
- infrastructure tooling for API discovery, API GUIs, API documents, automated quality checks


## Conventions used in these guidelines
The requirement level keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT",
"RECOMMENDED", "MAY", and "OPTIONAL" used in this document (case insensitive) are to be interpreted as 
described in RFC 2119.

## General API Guidelines

- MUST follow API first principle
- MUST provide API specification using OpenAPI
- SHOULD provide API user manual

### REST Basics - Meta Information

- MUST contain API meta information
- MUST use semantic versioning
- MUST provide API identifiers
- MUST provide API audience (internal, external, partner etc.)


### REST Basics - Security

- MUST secure endpoints
- MUST define scopes
- MUST follow a standard naming convention for scopes (permission)


### REST Basics - Data Formats

- MUST use standard formats for dates, number and decimal
- SHOULD only use UUIDs if necessary


### REST Basics - URL

- MUST pluralize resource names
- MUST use user-friendly resource identifiers
- MUST use kebab case for path segments

`/shipment-orders/{shipment-order-id}`
- SHOULD limit the number of sub-resource levels
- MUST use snake case for query parameters


### REST Basics - JSON payload

- MUST use JSON as the payload interchange data format
- SHOULD design single resource schema for reading and writing
  - To simplify API specs and API maintenance, as well as the cognitive load of developers, endpoints 
    should utilize a common model for reading and writing the same resource type. The differences between 
    read and write models are best addressed by
        - marking properties writeOnly that are only available in a request, e.g. passwords, and 
        - marking properties readOnly that are only available in a response, e.g. resource identifiers.
- SHOULD use standard media types
- SHOULD pluralize array names
- SHOULD define maps using `additionalProperties`

### REST Basics - HTTP requests

- MUST use HTTP methods correctly (GET, PUT, POST, PATCH, DELETE)
- MUST fulfill common method properties
  - safe- the operation semantic is defined to be read-only, meaning it must not have intended side effects, 
    i.e. changes, to the server state.
  - idempotent - the operation has the same intended effect on the server state, independently whether it is 
    executed once or multiple times. Note: this does not require that the operation is returning the same 
    response or status code.
  - cacheable - to indicate that responses are allowed to be stored for future reuse. In general, requests
    to safe methods are cacheable, if it does not require a current or authoritative response from the server.
- SHOULD consider to design POST and PATCH as idempotent. Please refer API Idempotency section for more details

### REST Basics - HTTP status codes

- MUST use official HTTP status codes
- MUST specify success and error responses

### REST Basics - HTTP headers

- MUST use code 429 with headers for rate limits
- MAY consider to support ETag together with If-Match/If-None-Match header
- MAY consider to support Idempotency-Key header

#### Internal API Headers

Request headers
- authorization
  - required
- channel-type
  - required
- request-id
  - required
- trace-id
  - required
- user-agent
  - Optional
- idempotency-key
  - Optional
  - Ref: https://datatracker.ietf.org/doc/draft-ietf-httpapi-idempotency-key-header/
- request-timestamp
  - Optional
- path-params
  - Optional
- query-params
  - Optional

Response headers
- cache-control
  - Optional
  - Set to "No-Cache; No-Store" when caching is not needed
- idempotency-key
  - Optional
- idempotency-replayed
  - Optional
- idempotency-expiry
  - Optional
- client-should-retry
  - Optional

#### External API Headers
- request-id
  - required
- trace-id
  - required
- client-id
  - required
- user-agent
  - Optional
- idempotency-key
  - Optional
  - Ref: https://datatracker.ietf.org/doc/draft-ietf-httpapi-idempotency-key-header/
- request-timestamp
  - Optional
- path-params
  - Optional
- query-params
  - Optional

Response headers
- cache-control
  - Optional
  - Set to "No-Cache; No-Store" when caching is not needed
- idempotency-key
  - Optional
- idempotency-replayed
  - Optional
- idempotency-expiry
  - Optional
- client-should-retry
  - Optional

### REST Design - Performance

- SHOULD reduce bandwidth needs and improve responsiveness
- SHOULD use Gzip compression
- SHOULD partial responses via filtering

### REST Design - Pagination

- MUST support pagination
  - There are two well known page iteration techniques:
    - Offset-based pagination: numeric offset identifies the first page-entry
    - Cursor-based pagination — aka key-based pagination: a unique key identifies the first page-entry 
      (see also Twitter API or Facebook API)
- SHOULD prefer cursor-based pagination, avoid offset-based pagination

### REST Design - Compatibility

- MUST not break backward compatibility


### Versioning
All APIs MUST be versioned. The API URL MUST contain the version reference.

#### Major Version Numbers
The major version numbers MUST be v1, v2, v3. 

#### When to version an API
A new API MUST be versioned v1 when it goes to PROD for the first time. The major version MUST be changed if

- The interface changes (either the input or the output, including headers). If the changes doesn't introduce a breaking change to the consumers then it doesn't require a major version change.
  - Producers MUST be able to make non-breaking changes without the need to change the schema version
  - Consumers MUST be able to consume the non-breaking changes without the need for the producer to change the schema version
- The API business logic is changing significantly that it will alter the behavior of the API and will affect how the client applications use the API
- If the API URI or the resources it accesses are changing, then it is a new API.

#### Multiple version support

- Atleast <> versions of the API MUST be supported
- The deprecated APIs MUST be supported for a period of <> days/months/years

#### Minor version support

When there are no breaking changes to the interface or the business logic (e.g., v1.1, v1.2 etc.)

### Handle all downstream service timeouts elegantly

- Timeouts MUST be set on all downstream service calls  appropriately
- Depending on use case, retries MUST be attempted
- Also depending on the use case, it may be OK to send back cached data from the previous call rather than HTTP 500
- HTTP status code 500 SHOULD be returned in the response if the API could not be completed due to timeouts

### Handle all PII data securely

- API MUST not return any PII data in plain text
- PII data must masked if returned for external consumption
- PII data used for future reference by external consumers SHOULD be encrypted 

### Implement validation and cleansing of all input data
To prevent any security vulnerabilities, all input data MUST be validated and cleansed

- Input validation is performed to minimized malformed data from entering the system
- The REST service MUST perform a detailed validation of the data types for each incoming field based on the business logic
- HTTP status code 400 with appropriate failure description SHOULD be returned
- Use of standard validators for common data inputs like emails, IP Address, Credit card numbers, URL datetime etc.
- Any input data that passes validation SHOULD be cleansed to avoid injection attacks
- Unsafe characters MUST be removed from inputs (using RegEx)

### Implement end-to-end traceability for a single API call

- Implement a common approach to trace the API calls end-to-end
- SHOULD use traceId in the header for every call


### Expose a ping endpoint for health check

- All APIs MUST expose a /ping endpoint at the root of the service for health check
- A blank response with 200 OK HTTP status code SHOULD be returned
- The Cache-Control header from the service SHOULD be "No-Cache; No-Store"

### Documentation

- All APIs MUST be documented in Open API format using OAS 3.x specification
- Refer to http://swagger.io/specification

### Developer and pipeline linting

- Use spectral ruleset for VSCode or Intellij for OAS linting
- The default ruleset can be used (or) we can create a custom ruleset for linting
- Examples of rules
  - Any integer type SHOULD have at least a min valud defined
  - Any ID SHOULD have uuid format
  - Any date MUST have a format of date or datetime
  - Parameters MUST have a description
  - Responses MUST have a description
  - String values SHOULD have a RegEx pattern defined
  - Response code validations
  - Use of E-Tag for concurrency
  - Check for Idempotency headers in request and response
  - Allowed headers

Reference

- https://docs.stoplight.io/docs/spectral/e5b9616d6d50c-rulesets