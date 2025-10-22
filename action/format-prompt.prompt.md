# .prompt.md

## Title

Specification for `.prompt.md` — A Standard for AI-Generated Optimized Prompts

## Objective

Define a structured format that enables an AI model (e.g., GPT-5) to transform a short task description into a complete, optimized prompt ready for direct use.

## Purpose

Guide AI systems to:

- Extract intent, context, and constraints from minimal input.
- Produce prompts that are structured, precise, and aligned with the user’s goals.
- Eliminate ambiguity and ensure consistent, reproducible results.

---

## Input Fields

| Field        | Description                                       |
| ------------ | ------------------------------------------------- |
| **GOAL**     | Core purpose of the task.                         |
| **CONTEXT**  | Audience, domain, and constraints.                |
| **DATA**     | Provided materials (text, code, tables, etc.).    |
| **STYLE**    | Tone, register, persona, and language.            |
| **FORMAT**   | Desired output structure (Markdown, JSON, etc.).  |
| **TOOLS**    | Allowed model tools or APIs.                      |
| **EVAL BAR** | Evaluation criteria and success metrics.          |
| **LIMITS**   | Word/token bounds, ethical or safety constraints. |
| **EXAMPLES** | Positive/negative examples if any.                |

If essential fields are missing, the model must infer minimally and state **ASSUMPTIONS**.

---

## Expected Output

The model returns **one fenced code block** containing the **final optimized prompt** only — no commentary or explanation outside the fence.

---

## Output Prompt Structure

### 1. System

- Define model identity, scope, and safety policy.
- Require short rationale bullets only.
- Forbid explicit chain-of-thought.

### 2. Role

- Domain expertise and success criteria.

### 3. Task

- Clear, measurable deliverable definition.
- Include the DONE condition.

### 4. Context

- Describe audience, locale, timezone, and relevant background.

### 5. Inputs

- Declare variable placeholders (e.g., `{{GOAL}}`, `{{DATA}}`).

### 6. Constraints

- Style rules, formatting, citations, prohibitions, and limits.

### 7. Tools (optional)

- Allowed tools, their input/output specifications.

### 8. Process

- Ordered steps: plan → execute → verify → format → output.
- Ask at most three clarifying questions if necessary, else proceed with **ASSUMPTIONS**.

### 9. Quality Checklist

- Verify goal satisfaction, constraint adherence, and formatting accuracy.

### 10. Output Format

- Provide exact schema or Markdown layout required for output.

### 11. Evaluation Rubric

- 0–5 scoring for **Clarity**, **Fidelity**, **Constraints**, **Correctness**, **Formatting**.
- Minimum acceptable score: ≥4.

### 12. Examples (optional)

- Include 1–2 consistent few-shot examples.

### 13. Assumptions

- List any inferred or missing details.

---

## Algorithm for Prompt Construction

1. Parse `GOAL`, `CONTEXT`, `DATA`, `STYLE`, `FORMAT`, `TOOLS`, `EVAL BAR`, `LIMITS`.
2. Define placeholders.
3. Select an appropriate **STYLE** profile.
4. Generate explicit **Constraints** and **Output Format**.
5. Add **Process** and **Checklist** sections.
6. Embed examples if needed.
7. Return only the completed prompt block.

---

## Model Constraints

- Must be GPT-5 compatible.
- No hidden prompts, keys, or tokens.
- Avoid “think step-by-step”; instead, use structured reasoning.
- Deterministic, scoped, and bounded outputs.
- Always produce runnable code for programming tasks.

---

## Anti-Patterns

- Undefined success criteria.
- Vague instructions or missing formats.
- Overly open-ended reasoning.
- Inconsistent examples or locale omissions.

---

## Templated Skeleton

```text
System:
- You are {{ROLE}}. Operate within {{LIMITS}}. Provide brief rationale bullets only. No chain-of-thought.

Role:
- Expert in {{DOMAIN}} producing {{ARTIFACT}} that meets {{EVAL_BAR}}.

Task:
- Produce {{DELIVERABLE}} to achieve {{GOAL}}.

Context:
- Audience: {{AUDIENCE}}. Locale: {{LOCALE}}. Timezone: {{TIMEZONE}}. Details: {{CONTEXT}}.

Inputs:
- {{DATA_SPEC}}
- Variables: {{VARIABLES_LIST}}

Constraints:
- Style: {{STYLE}}. Length: {{LENGTH_LIMIT}}. Citations: {{CITATION_RULES}}. Prohibited: {{PROHIBITIONS}}.

Tools (optional):
- {{TOOLS}} with contracts {{TOOL_CONTRACTS}}.

Process:
1. Plan
2. Execute
3. Verify vs {{EVAL_BAR}}
4. Format as {{FORMAT}}
5. Output
If data missing, ask ≤3 questions or proceed with **Assumptions**.

Quality Checklist:
- Goal met?
- Claims supported?
- Format correct?
- Edge cases covered?
- Safety rules respected?

Output Format:
- {{OUTPUT_SCHEMA_OR_MARKDOWN_TEMPLATE}}

Evaluation Rubric:
- Clarity, Fidelity, Constraints, Correctness, Formatting ≥4/5.

Examples (optional):
- {{FEW_SHOT_EXAMPLES}}

Assumptions:
- {{ASSUMPTIONS_LIST}}
```

---

## Examples

### Example 1 — Product Requirements Prompt

**Brief:** Generate a concise PRD prompt for a mobile habit tracker.

**Resulting Optimized Prompt:**

```text
System:
- You are a staff product manager. Rationale bullets only. No chain-of-thought.

Role:
- Expert in PRD writing for mobile applications.

Task:
- Create a Markdown PRD for a mobile habit tracker.

Context:
- Audience: senior engineers, PMs. Locale: en-US. Platform: iOS & Android.

Inputs:
- {{App name}}, {{User segment}}, {{Key constraints}}

Constraints:
- ≤800 words, concise technical tone, structured Markdown.

Process:
1. Define problem, goals, non-goals.
2. Outline users, scenarios, and risks.
3. Validate measurability of goals.
4. Format and output.

Quality Checklist:
- Clear goals? Non-goals explicit? Format correct?

Output Format:
## Problem
## Goals
## Non-Goals
## Users
## Scenarios
## Requirements
## Risks
## Open Questions

Assumptions:
- Default name “HabitRay”, users = “busy professionals”.
```

### Example 2 — Python Code Prompt

**Brief:** Generate a Python 3.11 script to parse Nginx logs into Parquet.

**Resulting Optimized Prompt:**

```text
System:
- You are a senior Python engineer. No chain-of-thought.

Role:
- Build production CLI and test suite.

Task:
- Write complete Python script that parses Nginx logs into Parquet with tests.

Context:
- Offline environment, Python 3.11, local I/O.

Inputs:
- {{LOG_PATH}}, {{OUTPUT_FILE}}

Constraints:
- Stdlib + pyarrow only, fully typed, black-compatible, no placeholders.

Process:
1. Define schema. 2. Implement CLI. 3. Add parser + pytest. 4. Output file tree then code.

Quality Checklist:
- Tests pass? CLI usable? Handles malformed lines?

Output Format:
Markdown tree + code blocks for each file.

Assumptions:
- Default output `./nginx.parquet`.
```

### Example 3 — Executive Summary Prompt

**Brief:** Summarize a 20-page AI governance report for executives (200 words).

**Resulting Optimized Prompt:**

```text
System:
- You are a policy analyst. Rationale bullets only.

Role:
- Create a concise executive summary.

Task:
- Summarize PDF into ≤200 words + 5 risks + 5 mitigations.

Context:
- Audience: executives. Locale: en-GB.

Inputs:
- {{PDF_TEXT}} with page markers.

Constraints:
- Cite pages as (p. X). No speculation.

Output Format:
**Summary (≈200 words)**
**Top Risks (5)**
**Mitigations (5)**
```
