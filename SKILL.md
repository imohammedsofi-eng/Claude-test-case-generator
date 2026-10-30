---
name: test-case-generator
description: Generates structured, traceable software test cases from requirement documents (BRD, SRS, PRD, user stories, acceptance criteria, API specs). Use this skill whenever the user shares or pastes requirements and asks for test cases, test scenarios, a test design, a test plan, QA coverage, a traceability matrix, or says things like "write tests for this feature", "what should I test", or "turn these user stories into test cases", even if they don't use the words "test case". Outputs Excel, CSV, or Markdown ready to import into Jira, Xray, TestRail or Zephyr.
---

# Test Case Generator

Turn requirement documents into complete, traceable test cases using formal test design techniques, so a tester spends time reviewing instead of writing from scratch.

## Workflow

### 1. Read and parse the requirements
- Read the whole document first. Identify each discrete requirement and give it an ID. Reuse the document's own IDs (REQ-001, US-12, FR-3.2) when present; otherwise assign `REQ-01`, `REQ-02`, ...
- Note actors, preconditions, inputs, outputs, business rules, validations, error messages, and non-functional constraints (performance, security, accessibility).

### 2. Flag problems before generating
List, briefly, anything ambiguous, contradictory, untestable ("system should be fast"), or missing (no error handling, no limits on a field). Do not silently guess. Put these under an **Open Questions / Assumptions** section in the output, and state any assumption you made to proceed.

### 3. Pick design techniques per requirement
Read `references/techniques.md` and apply the techniques that fit:
- Equivalence partitioning and boundary value analysis for inputs and ranges
- Decision tables for combinations of business rules
- State transition for workflows and statuses
- Error guessing for common failure modes (nulls, special characters, duplicates, timeouts, permissions)

Cover each requirement with positive, negative, and boundary cases. Add non-functional cases only when the requirements imply them.

### 4. Write test cases
Use the schema in `references/output-format.md`. Every test case must have: ID, linked requirement ID, title, type (Positive/Negative/Boundary/Edge/Non-functional), priority (P1-P3), preconditions, numbered steps, test data, and a specific, verifiable expected result. Never write vague expectations like "works correctly".

Rules:
- One test case verifies one thing.
- Steps must be reproducible by someone who has never seen the app.
- Put concrete values in test data (e.g. `age = 17, 18, 65, 66`), not placeholders.
- Do not invent features, fields, or messages that are not in the requirements. If an expected message is unspecified, write `[Message not specified in requirements]`.
- Avoid padding: skip near-duplicate cases.

### 5. Add a traceability matrix and coverage summary
Map each requirement ID to its test case IDs. Flag any requirement with no coverage and explain why.

### 6. Deliver in the right format
- If the user names a format, use it.
- Default for more than ~15 cases: an `.xlsx` file (see `assets/template-columns.md`; use the xlsx skill if available) with sheets: Test Cases, Traceability, Open Questions.
- For small sets or quick questions: a Markdown table in chat.
- CSV on request, with columns matching Jira/Xray, TestRail or Zephyr import if the user names the tool.

End with a 3-4 line summary: number of cases by type, requirements covered, and the top open questions. Offer to expand any area (e.g. API, security, performance).

## Quality bar
Before delivering, check: every requirement is covered; every negative path implied by a validation rule has a test; every expected result is checkable; IDs are unique; no case contradicts the requirements.
