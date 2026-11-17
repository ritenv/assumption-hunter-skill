# Assumption Hunter

A portable Agent Skill for ChatGPT and Claude that detects consequential unsupported assumptions in AI-assisted planning, coding, and analysis.

## Modes
- **Audit (default):** read-only review, evidence classification, and concise recommendations.
- **Strict (opt-in):** request confirmation before actions dependent on high-impact unverified premises or blocking ambiguity.

## Usage examples
- "Use Assumption Hunter to audit this implementation plan."
- "Review this Git diff for unsupported assumptions."
- "Use Assumption Hunter in strict mode while planning this migration."

## Installation
Install the `assumption-hunter` directory as a skill in a host that supports Agent Skills, or provide `SKILL.md` and supporting references to your agent. Installation and automatic triggering differ between ChatGPT and Claude. Access to repositories, files, tests, or external sources depends on the host's tools and permissions.

## Contents
- `SKILL.md`: core workflow and mode rules
- `references/classification-guide.md`: classification examples and evidence hierarchy
- `templates/assumption-audit.md`: optional report template

## Limitations
This skill cannot guarantee that a model discovers every assumption. A model reviewing its own output may repeat errors. It must not claim independent verification without evidence. Strict mode is instruction-level, not a technical gate.

## Suggested validation
Compare with a plain "check your assumptions" prompt on examples with: a clear requirement (no false positive), ambiguous CSV export behavior, a payment webhook idempotency gap, and a destructive migration with unspecified retention rules. Measure useful findings, false positives, and unnecessary clarification questions.
