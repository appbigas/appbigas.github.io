# Agent Guide

This project uses an AI coding assistant during development. This guide captures
the expectations and workflow for collaborating with the agent in this repo.

## Workflow Overview

1. **Clarify the task.** Provide concise requirements, relevant context, and any
   constraints before the agent begins.
2. **Let the agent inspect.** The agent will gather repository context with
   read-only commands (`ls`, `rg`, `nl`, etc.) before editing.
3. **Review proposed changes.** The agent summarizes modifications, including
   affected files and suggested follow-up actions. Always read the diff before
   committing.
4. **Run validations locally.** If tests or builds are required, trigger them
   manually unless the agent explicitly reports running them.

## Editing Practices

- Default to ASCII when creating or updating files.
- Prefer incremental edits via `apply_patch`; avoid wholesale rewrites unless
  approved.
- Add comments sparingly—only where code is non-obvious.
- Never revert user-authored changes unless instructed.
- Respect existing formatting, linting, and file organization.

## Command Usage

- Prefix shell commands with `bash -lc` and set the working directory via the
  `workdir` parameter.
- Prefer `rg`/`rg --files` for searches; fall back only if unavailable.
- Avoid destructive commands (e.g., `rm`, `git reset`) unless explicitly
  requested and reviewed.
- Assume sandboxed execution; request elevated permissions only when required
  for the task.

## Reviews and Summaries

- For code reviews, focus on correctness, regressions, and testing gaps before
  discussing stylistic issues.
- Final responses must be concise, reference touched files with paths, and list
  follow-up steps when appropriate.

## Troubleshooting

- If unexpected filesystem changes appear, pause and ask the user how to
  proceed.
- If a command fails due to sandboxing, report the failure and request
  guidance or approval before retrying.
- Keep the user informed about skipped tests or unmet assumptions.

Following these practices keeps collaboration with the agent predictable and
efficient for everyone working on the project.
