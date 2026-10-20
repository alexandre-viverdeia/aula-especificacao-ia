# Issue tracker: GitHub

Specs and tickets for this repo live as GitHub issues. Use the `gh` CLI for all operations; it infers the repo from `git remote -v`.

- **Create an issue**: `gh issue create --title "..." --body "..." --label ready-for-agent`. Use a heredoc for multi-line bodies. If the label is missing, create it first: `gh label create ready-for-agent --description "Pronta para o agente"`.
- **Read an issue**: `gh issue view <number> --comments`.
- **List issues**: `gh issue list --state open --json number,title,labels`.
- **Comment on an issue**: `gh issue comment <number> --body "..."`.
- **Close**: `gh issue close <number> --comment "..."`.
- **Blocking**: put a `Blocked by: #<n>, #<n>` line at the top of the ticket body. A ticket is unblocked when every listed issue is closed.

## When a skill says "publish to the issue tracker"

Create a GitHub issue.

## When a skill says "fetch the relevant ticket"

Run `gh issue view <number> --comments`.
