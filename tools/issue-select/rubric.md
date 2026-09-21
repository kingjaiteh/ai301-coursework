# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | repo-facts block: the "last 5 default-branch commits" list, both dates and author names | At least 3 of the 5 commits are dated within 30 days of the capture date and are authored by non-bot accounts (a username ending in `[bot]` counts only if the commit merges a human's PR) | required |
| repo-in-use | repo-facts block: "archived:", "latest release", "last push to any branch" | `archived` is no, and either the latest release or the last push to any branch falls within 90 days of the capture date | required |
| ai-policy-ok | repo-facts block: the "contribution policy" line | The policy does not ban AI-assisted contributions. Stated conditions (disclosure, personal understanding, testing, human review) pass; no policy stated passes | required |
| unclaimed | repo-facts block: "this issue: assignees:" and "linked PRs:", plus the Comments section | No assignee recorded, no open linked PR, and no claim comment ("I'll take this", "can I work on this", "working on this") left standing without a maintainer closing it out | required |
| scope-fits-newcomer | Issue body and Comments section | Passes unless one of the four scope failures is present: the issue is explicitly an umbrella or tracking issue whose sub-items are meant to be split out, the thread shows a design still being debated with no owner/member/collaborator settling it, a maintainer states the work requires changes to core internals, or the issue is a pure usage or support question | required |
| target-named | Issue body | The body names at least one concrete target of the work: a file, a page, a function, a command, or an acceptance-criteria checklist | required |
| issue-response-latency | repo-facts block: the "maintainer first-response sample" | At least 3 of the 5 sampled threads drew a maintainer reply, or the median days-to-first-reply across the sample is under 30 | preferred |
| low-setup | Issue body: the areas and file types the work touches | The work is confined to documentation, tests or configuration, or can otherwise be completed without standing up the project locally | preferred |
| bounded-deliverables | Issue body: the changes it enumerates | 6 or fewer discrete deliverables, none of which introduces a new dependency, schema, or public API | preferred |
| stack-familiar | repo-facts block: the repo description, plus the file extensions named in the issue body | The work is in Python, SQL, JavaScript, TypeScript, or prose and documentation | preferred |

## Verdict rule

Accept if every required check passes. Preferred checks never change the
verdict; they rank accepted issues in fit order, best fit first.

Unclear counts as **fail** on the four repo-facts checks — maintainer-alive,
repo-in-use, ai-policy-ok and unclaimed. Every bundle carries a repo-facts
block, so a signal missing from it is a real absence rather than a gap in
the capture, and a first issue has to prove itself on those four.

Unclear counts as **pass** on the two judgment checks, scope-fits-newcomer
and target-named. The evidence guide warns that a terse writeup is not the
same as an unscoped one: a short body, a bare acceptance checklist, or a bug
report without reproduction steps can still be a perfectly bounded first
issue. These two grade the size of the work being asked for, not the polish
of the description, so ambiguity in the writing is not held against the
issue.