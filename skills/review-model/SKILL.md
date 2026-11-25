---
name: review-model
---

- Review:
  - Associations
  - Validations (e.g. empty string, inclusion, negative/positive)
  - State transitions
  - Redacting/encryption
  - Concerns
- Only validate things not already validated by the schema if the error would be surfaced to users
- Consider leveraging timestamps for state transitions
- Use enum library to get helpers (e.g. validation, list of values, negate scopes)
  - Disable instance methods when using with state transitions to avoid conflicting methods
