## Pull Request

### Summary
_What does this PR do? (1–3 sentences)_

### Related Task
Closes `<!-- e.g. AUTH-01 -->`

### Domain / Module
- [ ] auth
- [ ] catalog
- [ ] playback
- [ ] billing
- [ ] ingestion
- [ ] frontend
- [ ] infra
- [ ] docs

### Type of Change
- [ ] ✨ New feature
- [ ] 🐛 Bug fix
- [ ] ♻️ Refactor
- [ ] 📦 Dependency / tooling update
- [ ] 📝 Documentation
- [ ] 🧪 Tests only

---

### Checklist
- [ ] Code compiles without warnings (`mvn verify` / `pnpm build`)
- [ ] New unit tests added (or existing tests cover the change)
- [ ] All existing tests pass
- [ ] No hardcoded secrets or credentials
- [ ] Flyway migration script added (if schema changed), named `V<next>__<description>.sql`
- [ ] API changes documented (OpenAPI / Swagger annotations updated)
- [ ] `TASK_BOARD.md` updated — task moved to Done
- [ ] `DECISIONS.md` updated (if an architectural decision was made)

---

### Testing Instructions
_How should a reviewer test this change locally?_

```
# Example:
mvn test -pl backend/auth
# or
cd frontend && pnpm test
```

---

### Screenshots / Recordings _(if UI change)_
_Paste screenshots or a Loom/gif link here_

---

### Notes for Reviewer
_Anything specific you want the reviewer to focus on?_
