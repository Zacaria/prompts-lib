# Preserve work on GitHub and clean the workspace

Applies to all projects, including projects with real users.

Use GitHub as durable storage, not the local workspace.

## During the work
- Commit and push useful progress at meaningful checkpoints, including before pausing or handing off unfinished work. Label unfinished checkpoints clearly.
- Use a source work branch authorized by the project's existing permissions. A preservation push must not bypass review or trigger an unauthorized deployment or publication.
- Keep temporary files in the task-owned workspace, not scattered across other directories.

## Before finishing
1. Inspect every file created by the task, including untracked and ignored files.
2. Commit and push useful source, tests, scripts, documentation, decisions, and evidence needed to understand, verify, or resume the work.
3. Once no active process, reviewer, or job needs them, delete disposable files: caches, dependencies, reproducible build outputs, obsolete experiments, duplicate copies, and unnecessary logs or captures. Do not commit them merely to make the workspace look clean.
4. Verify that GitHub contains the expected branch, commit, and retained artifacts. A local commit or an attempted push is not enough.
5. Remove task-owned temporary workspaces through the native cleanup mechanism once no active process, reviewer, or job needs them.

## Boundaries
- Never commit secrets, credentials, private customer data, or unsanitized evidence. Preserve protected inputs in their approved secure storage.
- Preserve other people's work and pre-existing changes. Do not delete files merely because Git does not track them.
- If preservation or cleanup is blocked, keep the necessary files, report the exact blocker and remaining paths, and do not claim cleanup is complete.

## Done means
- Useful work is verified on GitHub.
- No task-created intermediate files remain untracked or ignored, including outside the repository.
- Report what was preserved, what was deleted, and what remains blocked.
