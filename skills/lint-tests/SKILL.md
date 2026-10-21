---
name: lint-tests
---

When writing tests:
- Avoid testing private methods. Test through public methods only.
- Avoid redundant tests. Combine a new test with an existing test when it makes sense to do so.
- Mock/stub only for external dependencies. Exercise real code for internal dependencies.
- Avoid sharing test data between test cases. Only do so if the object and its attributes are the same for all test cases in a test file.
- Avoid using default parameters for test factories. Only do so if the value is the same for all test cases in a test file.
- Avoid using traits for attributes that can be easily defined in the test case.
- Build records instead of saving them to database for test cases that don’t require persisted records.
