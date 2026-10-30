# Test Case Generator (Claude Skill)

A custom [Claude Skill](https://www.anthropic.com/news/skills) that converts requirement documents (BRD, SRS, PRD, user stories, acceptance criteria) into structured, traceable test cases, cutting manual test design time.

## What it does
- Parses requirements and assigns IDs
- Flags ambiguous, untestable, or missing requirements before writing tests
- Applies formal techniques: equivalence partitioning, boundary value analysis, decision tables, state transition, error guessing
- Produces positive, negative, boundary, and edge cases with concrete test data and verifiable expected results
- Builds a requirement-to-test traceability matrix and an open-questions list
- Exports to Excel, CSV, or Markdown (importable into Jira/Xray, TestRail, Zephyr)

## Structure
```
test-case-generator/
├── SKILL.md                    # Instructions and trigger description
├── references/
│   ├── techniques.md           # Test design techniques and checklists
│   └── output-format.md        # Test case schema and examples
├── assets/template-columns.md  # Excel layout
└── examples/sample-requirements.md
```

## Install
1. Download `test-case-generator.skill` from Releases (or zip the `test-case-generator` folder).
2. In Claude: Settings > Capabilities > Skills > Upload skill.
3. Enable it, then start a chat.

## Usage
Attach or paste a requirements doc and ask:
> "Generate test cases from this SRS and give me an Excel file with a traceability matrix."

## Results
_Add your measured numbers here, e.g. "Test design for a 20-requirement SRS: 3 hrs manual vs 25 min with skill + review."_

## Limitations
Output is a draft: a QA engineer should review it. Quality depends on requirement clarity.

## License
MIT
