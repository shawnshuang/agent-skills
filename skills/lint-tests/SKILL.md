---
name: lint-tests
---

When writing tests:
- Avoid testing private methods. Test through public methods only.
- Avoid redundant tests. Combine a new test with an existing test when it makes sense to do so.
- Mock/stub only for external dependencies. Exercise real code for internal dependencies.
- Avoid sharing test data between test cases. Only do so if the object and its attributes are the same for all test cases in a test file.
- Define helper methods to make tests easier to read. The helper methods should define attributes, but only if they don't change for any of the test cases. For the ones that do, they should be passed as arguments to the helper method.
- Avoid using traits for attributes that can be easily defined in the test case.
- Build records instead of saving them to database for test cases that don’t require persisted records.
