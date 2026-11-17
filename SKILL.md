---
name: assumption-hunter
description: Identify consequential unsupported assumptions in requirements, plans, code changes, and AI-generated answers; distinguish evidence from inference, assess risk, and request clarification only when necessary. Use when requirements are ambiguous, important decisions rely on unstated premises, or reviewing an implementation for assumption-driven mistakes.
---

# Assumption Hunter

Detect and manage **consequential unsupported assumptions**, without turning every ambiguity into a question. Default to **audit** mode; use **strict** mode only when explicitly requested.

## Inputs and boundaries

Use the user's request and any available specifications, repository files, code, tool results, and decisions. Do not claim access to missing context. Do not fabricate citations, tests, confirmations, or requirements. Treat explicit user statements as requirements, not assumptions. Later explicit decisions supersede earlier ones when clearly applicable.

## Workflow

1. **Extract the contract.** Briefly identify the requested outcome, stated constraints, and acceptance criteria. Quote or reference exact supporting evidence when available.
2. **Find hidden premises.** Inspect decisions about data, environment, users, permissions, API behavior, scale, dependencies, edge cases, security, performance, and semantics. Look for choices presented as facts without supporting evidence.
3. **Challenge each candidate.** Ask: Is it explicitly stated? Verified by available evidence? A safe, reversible convention? Or an unsupported leap? Seek disconfirming evidence where feasible.
4. **Rank materiality.** Consider probability of being wrong, impact if wrong, reversibility, and cost of checking. Focus on high-impact premises; omit trivial stylistic choices.
5. **Choose an action.** Verify using available tools; ask one targeted question if the missing answer blocks safe progress; otherwise state a provisional assumption and proceed with a reversible approach. Do not invent tool execution.
6. **Report concisely.** Use the format below. Separate observed evidence from inference, and explain consequences.

## Classification

- **Confirmed**: Explicitly specified or supported by directly inspected evidence.
- **Reasonable default**: Not specified, but low-risk, conventional, and easy to change; disclose only if relevant.
- **Unverified**: Plausible but not established; verification or qualification needed.
- **Contradicted**: Conflicts with explicit requirements or reliable evidence.
- **Blocking ambiguity**: Material uncertainty where different interpretations lead to substantially different or unsafe outcomes.

Read `references/classification-guide.md` for examples and edge cases.

## Modes

### Audit (default)

Read-only analysis. Flag assumptions, evidence gaps, risks, and recommended actions. Do not modify code or files solely to perform an audit. If tools are unavailable, identify what remains unverified.

### Strict (explicit opt-in)

Before taking an action that depends on a **blocking ambiguity** or a high-impact **unverified** premise, request explicit user confirmation. Continue on low-risk, reversible defaults without excessive interruptions. Strict mode is an instruction-level guard, not a guaranteed runtime enforcement mechanism.

## Output format

Use this format when meaningful issues exist; omit empty sections:

**Assumption audit — [subject]**

- **Finding:** [specific implicit premise]
  - **Status:** [classification]
  - **Evidence:** [source, inspected artifact, or “none available”]
  - **Risk:** [what could go wrong and why it matters]
  - **Next step:** [verify / ask / qualify / use reversible default]

**Blocking question:** [one precise question, only if necessary]

**Safe path:** [minimal approach that does not depend on unsupported high-risk claims]

If no material issues are found, say so without asserting the work is error-free.

## Rules

- Do not confuse a hypothesis with a fact or an explicit requirement with an assumption.
- Do not require citations for trivial coding conventions or stylistic choices.
- Do not assume a missing requirement is permission to introduce new functionality.
- Never silently resolve consequential ambiguity in the agent's favor.
- Do not fabricate risk scores or false precision.
- Do not turn an audit into an implementation unless asked.
- When reviewing code, reference file paths and line numbers if actually available.
- Distinguish model-only reasoning from independent verification.
