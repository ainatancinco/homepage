# Notes for Claude

## No internal IDs or `claude/` references
Don't cite plan, review or test IDs (`IL-19`, `RT-3`, `SEC-12`, `R3`, `Q14`, `A2`) or paths to `claude/` files (`claude/todo/idle-logout-plan.md`) in code, comments, test names, committed docs, commits or PRs. `claude/` is gitignored, so readers can't open it. Say what it does or why instead (`"the × close button calls onStay"`, `"hidden until custom SMTP is set up"`).
- OK: common abbreviations (MFA, JWT, RLS), codes from a committed table (`docs/error-codes.md`), paths to committed files (`docs/runbook.md`), and anything inside `claude/` itself.
- When you edit a file, remove any such IDs and `claude/` references from all of it (no behaviour change) and mention it. Don't edit other files just for this, and never edit an applied migration.

## Workflow
- Don't commit or push. After a change, run `pnpm test:run` and `pnpm typecheck`, then end with a one-line summary and a commit message (`feat:`/`fix:`/`chore:`/`docs:`/`test:`, short body, no internal IDs).
- Give commit messages and PR descriptions ready to copy and paste: each in its own code block holding exactly the text to paste. Fence a PR description (Markdown) with four backticks so the backticks inside it survive. Put the PR title outside the block.
- Plans live in gitignored `claude/todo/*.md`. When the user decides something that changes or adds to a plan, record it in that plan's Decisions table in the same change, so a later session doesn't undo it.
- Test coverage: aim for 85% or better overall in `pnpm test:coverage` (statements, branches, functions and lines). New or changed code comes with tests, and a change shouldn't lower coverage.
- Before stating how the app behaves, check the code (and run it or a test where you can); say when something is unverified.

## Comments
Let names and code say what happens; comment only what the code can't show:
- why it's done this way when the obvious way is wrong (a gotcha, a race, a library quirk, a security trade-off);
- a constraint or decision a later change must not undo (and where it's decided, e.g. a docs page).
No comments that restate the code, label sections, or narrate a change. Keep them to one or two lines. When you edit a file, delete redundant comments in the code you touch, but don't strip comments across a file just for this.
