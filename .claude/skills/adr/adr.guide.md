# Architecture Decision Records (ADR) Guide

A practical guide to writing and maintaining effective ADRs.

---

## What is an ADR?

An **Architecture Decision Record** (ADR) is a short document that captures a significant decision made during a project, along with its context and consequences.

> *"ADRs are like a decision journal — they answer the question: Why did we do it this way?"*

**Key terms:**
- **AD** — Architecture Decision
- **ADR** — Architecture Decision Record (the document)
- **ADL** — Architecture Decision Log (collection of all ADRs)

---

## Why Use ADRs?

| Benefit | Description |
|---------|-------------|
| **Preserve context** | Decisions make sense when made, but context fades over time |
| **Onboard faster** | New team members understand past decisions without archaeology |
| **Avoid rehashing** | Stop revisiting the same decisions when people forget why |
| **Enable evolution** | Know what can safely change vs. what has deep dependencies |
| **Improve quality** | Writing forces clarity; review improves decisions |

---

## When to Write an ADR

✅ **Write an ADR when:**
- Choosing between technologies (framework, database, language)
- Defining integration patterns or API approaches
- Making security or compliance decisions
- Establishing coding standards or conventions
- Deciding on deployment or infrastructure strategies
- Any choice that future developers will wonder about

❌ **Skip an ADR when:**
- The decision is trivial or easily reversible
- It's already covered by existing standards
- It's a temporary workaround with a clear expiration

> 💡 **Hint:** If you find yourself explaining a decision multiple times, it probably deserves an ADR.

---

## How to Write Each Section

### Status

Use one of these values:

| Status | Meaning |
|--------|---------|
| **Proposed** | Under discussion, not yet agreed |
| **Accepted** | Agreed and active |
| **Deprecated** | No longer recommended but not replaced |
| **Superseded** | Replaced by another ADR (link to it) |

> 💡 **Hint:** Mark superseded ADRs clearly — don't delete them. The history matters.

---

### Context

This is the **most important section**. Capture:

1. **The problem** — What situation requires a decision?
2. **Constraints** — Budget, time, skills, existing systems
3. **Forces** — Competing priorities, trade-offs at play
4. **Assumptions** — What are you taking for granted?

**Good context example:**
> We need to choose a database for our new microservice. The team has strong PostgreSQL experience, but leadership wants consistency with our existing MongoDB stack. Response time is critical — queries must return in under 50ms.

**Bad context example:**
> We need a database.

> 💡 **Hint:** Write context as if explaining to someone joining the team six months from now.

---

### Decision

State the decision clearly using **active voice**:

✅ **Good:** "We will use PostgreSQL because it meets our performance requirements and matches team expertise."

❌ **Bad:** "PostgreSQL was selected." (passive, no rationale)

**Formula:**
> We will **[action]** because **[reason]**.

> 💡 **Hint:** If you can't articulate the "because," the decision may not be ready.

---

### Alternatives Considered

List the options you evaluated. For each:
- Brief description
- Key pros and cons
- Why it was or wasn't chosen

**Be fair to rejected options.** Listing only strawmen weakens the ADR.

> 💡 **Hint:** If there was only one option, question whether an ADR is needed — or whether you explored enough.

---

### Consequences

Be honest. List **all** impacts, not just positives:

| Type | What to capture |
|------|-----------------|
| **Positive** | Benefits, improvements, new capabilities |
| **Negative** | Trade-offs, limitations, technical debt |
| **Neutral** | Changes that are neither good nor bad |
| **Risks** | What could go wrong? How will you mitigate it? |

> 💡 **Hint:** Negative consequences aren't failures — they're acknowledged trade-offs. Hiding them helps no one.

---

## File Naming Convention

Use a consistent format:

```
docs/adr/
├── 0001-use-postgresql-for-user-service.md
├── 0002-adopt-rest-over-graphql.md
├── 0003-implement-circuit-breaker-pattern.md
└── README.md  (index of all ADRs)
```

**Format:** `NNNN-short-lowercase-title.md`

- Sequential numbers (0001, 0002...)
- Present-tense verb phrases
- Lowercase with hyphens
- `.md` extension

> 💡 **Hint:** Never reuse numbers. If ADR-0005 is superseded, create ADR-0012, not a new 0005.

---

## Best Practices

### Writing Tips

1. **Keep it short** — 1-2 pages maximum
2. **Write in full sentences** — No bullet fragments
3. **Be specific** — "PostgreSQL 15" not "a SQL database"
4. **Date everything** — Especially items that may change (costs, versions)
5. **One decision per ADR** — Split complex decisions into related ADRs

### Process Tips

1. **Write early** — Capture decisions when context is fresh
2. **Review together** — ADRs improve with discussion
3. **Store with code** — Keep ADRs in version control
4. **Update, don't delete** — Mark superseded, add amendments
5. **Schedule reviews** — Check ADRs quarterly for relevance

### Common Mistakes to Avoid

| Mistake | Why it's a problem |
|---------|-------------------|
| Too vague | "We chose the best option" helps no one |
| Too long | Walls of text don't get read |
| Post-facto rationalization | Write decisions, not justifications |
| Ignoring trade-offs | Makes the ADR seem like marketing |
| No alternatives | Suggests inadequate exploration |

---

## ADR Lifecycle

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  PROPOSED   │ ──▶ │  ACCEPTED   │ ──▶ │ SUPERSEDED  │
└─────────────┘     └─────────────┘     └─────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ DEPRECATED  │
                    └─────────────┘
```

1. **Proposed** — Draft created, shared for feedback
2. **Accepted** — Team agrees, implementation begins
3. **Deprecated** — Still valid but no longer recommended
4. **Superseded** — Replaced by a newer ADR

---

## Quick Reference Checklist

Before finalizing an ADR, verify:

- [ ] Title clearly describes the decision (not the problem)
- [ ] Status is set correctly
- [ ] Context explains why this decision was needed
- [ ] Decision uses active voice with clear rationale
- [ ] At least 2 alternatives were genuinely considered
- [ ] Consequences include both positive AND negative impacts
- [ ] File follows naming convention
- [ ] Related ADRs are linked

---

## Resources

- [Michael Nygard's original ADR blog post](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)
- [ADR GitHub Organization](https://adr.github.io/)
- [MADR Template](https://adr.github.io/madr/)
- [Joel Parker Henderson's ADR Repository](https://github.com/joelparkerhenderson/architecture-decision-record)

---

*Remember: The goal isn't perfect documentation — it's preserving just enough context for future decisions to be made wisely.*