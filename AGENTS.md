# Repository Guidelines

## Project Structure & Module Organization

This repository is a library of Markdown instructions for AI agents, rather than an application. Put task-specific prompts in `action/` and reusable agent setups or overlays in `setup/`. `init-modes.md` points readers to the multi-mode setup. `LICENSE` contains the repository license. There are currently no source-code, test, or asset directories.

## Development & Verification

There is no build system, dependency installation, or automated test suite in the repository. Edit the relevant Markdown file directly and review the result locally:

- `git diff --check` detects whitespace errors in tracked changes.
- `git diff -- path/to/file.md` shows the changes to a specific guide.
- `git status --short` identifies modified and new files before submission.

Preview Markdown in an editor when changing tables, lists, links, or fenced examples. Check that links and referenced paths resolve and that examples match the instructions around them.

## Writing Style & Naming

Use clear, direct instructions and preserve the structure and terminology of the file being edited. Organize longer prompts with descriptive headings, ordered steps, constraints, and explicit output formats where useful. Keep fenced examples and placeholders such as `{{GOAL}}` intact and consistent. Use lowercase, hyphen-separated filenames, following existing examples such as `setup/innovation-overlay.md`; use the `.prompt.md` suffix for prompts following that format. Match surrounding Markdown indentation and list style.

## Testing Guidelines

For a prompt change, manually walk through a representative input against the revised instructions. Check that the expected output is achievable, constraints do not conflict, and formatting requirements are unambiguous. Describe the scenario and result in the pull request. No coverage threshold or test naming convention is configured.

## Commits & Pull Requests

Recent commits use concise Conventional Commit prefixes, for example `feat: add actions` and `refactor: prompts organisation`. Use an imperative summary and keep each commit focused on one concern. In pull requests, explain the purpose and behavior change, link any relevant issue, and include the manual verification performed. Include before-and-after examples when they clarify a prompt change.

## Shared workspace rules

Read and follow the shared workspace policy for every project, including projects with real users.

@/home/hermes/repos/prompts-lib/AGENTS_WORKSPACE.md

## Shared building rules

Read the shared file below before changing this project. Its development rules apply only if the project has no real users yet; confirm that status before applying them. Existing project-specific security, data-preservation, and release requirements still apply.

@/home/hermes/repos/prompts-lib/AGENTS_BUILDING.md

Record project-specific corrections in this project's `## Lessons` section, not in the shared file.

## Lessons