# .prompt.md

## Title

Ingest and Contextualize External Prompt Content from a GitHub File

## Objective

Enable the AI model to fetch and incorporate the **raw content** of a prompt stored in a GitHub file (given its URL) into its working **context**, preserving structure, indentation, and formatting.

---

## Behavior Specification

### Inputs

| Parameter            | Type               | Description                                                                                                     |
| -------------------- | ------------------ | --------------------------------------------------------------------------------------------------------------- |
| **url**              | String             | The full GitHub URL of the target file (e.g., `https://github.com/user/repo/blob/main/path/to/file.prompt.md`). |
| **include_metadata** | Boolean (optional) | Whether to include file metadata (commit SHA, author, timestamp). Default: `false`.                             |

---

### Model Actions

1. **Validate** that the URL points to a raw or blob GitHub file.
2. **Transform** the `blob` URL into its `raw` equivalent if needed (`github.com/.../blob/...` → `raw.githubusercontent.com/.../.../...`).
3. **Fetch** the raw file contents.
4. **Inject** the fetched content into the model’s working context as `{{RAW_PROMPT_CONTENT}}`.
5. Optionally append metadata if `include_metadata = true`.
6. **Acknowledge** successful context extension without summarizing or altering content.

---

### Output

The model does not summarize or paraphrase the file. It must instead return:

```text
✅ Context updated with raw content from:
{{url}}

Content size: {{byte_count}} bytes
Metadata included: {{true|false}}
```

````

---

### Example Usage

**User Prompt**

```
Add to your context the raw content of the following prompt in this GitHub file:
https://github.com/example-org/ai-prompts/blob/main/templates/research_summary.prompt.md
```

**Model Actions**

1. Fetch `https://raw.githubusercontent.com/example-org/ai-prompts/main/templates/research_summary.prompt.md`
2. Insert the file content as `{{RAW_PROMPT_CONTENT}}` in memory.
3. Confirm update.

**Model Response**

```
✅ Context updated with raw content from:
https://github.com/example-org/ai-prompts/blob/main/templates/research_summary.prompt.md

Content size: 2,137 bytes
Metadata included: false
```

---

### Constraints

- Preserve full Markdown and code block fidelity.
- No summaries, truncations, or reformatting.
- Reject non-GitHub or inaccessible URLs with an explicit error message.
- Do not execute or interpret any code contained in the file.

---

### Failure Responses

| Condition     | Response                                         |
| ------------- | ------------------------------------------------ |
| Invalid URL   | ❌ `URL is not a valid GitHub file path.`        |
| Access denied | ❌ `Unable to access file at the specified URL.` |
| Empty content | ⚠️ `File fetched but appears empty.`             |

---

### Safety and Verification

- Only fetch from trusted GitHub domains.
- Strip credentials or tokens if present in the URL.
- Never auto-run fetched code or YAML instructions.

---

### Implementation Notes

- The raw file content becomes part of model memory under the key `RAW_PROMPT_CONTENT`.
- It can then be referenced by other prompt instructions using `{{RAW_PROMPT_CONTENT}}`.

---

### Example Follow-Up Usage

```
Now use {{RAW_PROMPT_CONTENT}} to generate an optimized prompt following the .prompt.md spec.
```
````
