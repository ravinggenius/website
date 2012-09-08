---
title: API Integration Testing
created_at: 2012-08-21 14:38:53 UTC
---

Different approaches to integration testing API interactions.


## Use real API

Test against an offsite, client-maintained, sandboxed API.

### Pros

* testing against a real api can provide better feeback from tests
* always stays in sync (hopefully)
* least amount of work to setup

### Cons

* api changes can break your tests, even without any code changes
* slow tests are evil
* difficult to start each test with known, consistent state


## Setup mock API

Test against an onsite, contractor-maintained fake API. API may be on office network as a shared service, or each developer may have separate copy.

### Pros

* testing against a "real" api can provide better feeback from tests
* can be faster than using the real api
* easier to keep tests and api syncronized

### Cons

* mock api may be out of sync with real api
* contractors now have two projects to maintain
* still pretty slow
* still difficult to reset state before each test


## Mock all the things

Build mock objects in tests for all external dependencies.

### Pros

* fast tests
* tests do not fail when api changes

### Cons

* hard to know what is being tested (*integration* test?)
* also difficult to inject a mock into server process (from test process)
* have to assume mocked responses are correct
* still need to hit actual api to verify tests
* tests do not fail when api changes


## Write custom connection layer (with in-memory store)

Build mock connection that gets swapped in when testing.

### Pros

* only mock what needs to be mocked
* fast tests
* tests do not fail when api changes
* easy to change (basic input/output)

### Cons

* have to assume mocked responses are correct
* still need to hit actual api to verify tests
* tests do not fail when api changes
