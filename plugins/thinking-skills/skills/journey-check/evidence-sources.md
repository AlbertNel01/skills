# Evidence sources

## North star (step 1) — ranked by authority

- **JIRA epic, then its stories** — Atlassian MCP `getJiraIssue` per key; `searchJiraIssuesUsingJql` with `parent = <EPIC-KEY>` to enumerate the children. Read Description, **Acceptance Criteria**, **Technical Criteria** (the code-facing half, and the easiest field to skip) and the **comments** — a mid-build scope change or a stakeholder's answer lives in comments, not in the body fields. Read the epic first, so each story's intent is read inside it.
- **Design doc in the repo** — `git -C <repo> show <base>:<path>`, rather than the working tree: docs get revised and sometimes retracted, and a local copy can be an abandoned revision.
- **Confluence page** — `getConfluencePage`. Check its revision history when the intent there looks newer than the ticket's.
- **Bug report and reproduction** — for a fix, the north star is the reproduction going green. Run it.
- **The user's originating request** — where no ticket exists. Quote it, then label it by where it lives: a request recorded in a repo doc or handoff is *unticketed*; one that lives only in the conversation is *unwritten*, and dies with the context.

A north-star item states an outcome, not a task: "recipients of a paused campaign stop receiving sends", not "add a paused check to the sender".

## Ground the repo (step 2)

Every repo on the list gets its own base branch; the working directory is often not a repo at all, so pass `-C <repo>` throughout.

```
git -C <repo> fetch --quiet origin
git -C <repo> symbolic-ref --short refs/remotes/origin/HEAD   # develop, main or master — differs per repo
git -C <repo> merge-base <base> HEAD
```

Fetch first: a stale base drags other people's merged commits onto the map as this journey's legs. A repo can also carry an abandoned `develop` alongside a `main` default, so take the base from `origin/HEAD` rather than by name.

## The three places (step 2)

- **Merged history** — GitHub MCP `search_issues` on the ticket key (`PROJ-1234 repo:<org>/<repo> is:pr`) or `list_pull_requests` filtered by head branch, then `get_pull_request`, `get_pull_request_files`, `get_pull_request_comments`. Once work is merged this is the only place the journey survives, and review feedback here is a common origin of legs nobody planned.
- **The branch** — `git -C <repo> log --oneline <merge-base>..HEAD`, then the same with `--name-only`; `git -C <repo> status --porcelain` for the working diff and untracked files. Work in flight is a leg, and the one no PR shows.
- **The unwritten** — the current task list, the plan for work not yet started, and decisions taken in this or a prior session. On a barely-started journey these are the only legs there are.

Two sweeps that catch legs the commands above miss: the sibling branches and other repos the tickets name (a leg often lives in the frontend repo and is invisible from the API one), and the date of the last commit — a branch stale by weeks may have had its north star moved or delivered elsewhere.
