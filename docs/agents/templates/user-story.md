# User Story Format

Standard format for writing a Jira-ready user story before formalizing a feature with a spec-driven workflow (e.g. `/speckit-specify`). This is the human-readable ticket that gets pasted into Jira; it is not a replacement for a formal spec document.

## Template

```
<short feature title>

As a <role>, I want <capability>, so that <benefit>.

**Glossary**:
- **<Term>**: <definition of any new domain term introduced by this story>

**Backend acceptance criteria**:
1. WHEN <trigger/condition>, THE SYSTEM SHALL <required behavior>.
2. ...

**Front-end acceptance criteria**:
1. WHEN <trigger/condition>, THE SYSTEM SHALL <required behavior>.
2. ...
```

## Notes

- Only include a Glossary section if the feature introduces a genuinely new domain term. Skip it otherwise.
- Acceptance criteria use EARS syntax (`WHEN ... THE SYSTEM SHALL ...`), one per numbered line, in both sections.
- Backend acceptance criteria are phrased around system/API behavior: status codes, validation, auth, persisted state.
- Front-end acceptance criteria are phrased around UI behavior: what's rendered, interaction states, inline validation feedback, not HTTP responses.
- Both sections live in the same story/ticket. Write the backend section first; if the frontend section depends on implementation details not yet finalized (endpoints, field names), share those as background rather than leaving the section blank.
