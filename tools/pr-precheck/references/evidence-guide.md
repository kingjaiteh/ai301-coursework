# Evidence guide: where evidence lives in a PR package

An eval bundle has five parts, in this order: **Repo facts**, **Issue**, **Thread highlights**, **Plan context** (the accepted plan with its repro evidence, files, scope, approach, test plan and any deviation note), and **Candidate PR** (Title, Description, Commits, Diff, Test evidence). In live mode the same evidence lives in the files named below.

## Plan fidelity (harness category: silent-drift)

**Where it lives.**
- Eval: the plan's scope sits in the Plan context block. Look for "Files:", "Not in scope:", the approach, and any "Deviation" or deferral note. What actually changed is in the Candidate PR's Diff (every `+++ b/<path>` line and every hunk). The description's claims about the change are in Title and Description.
- Live: the scope and deviation notes are in `plan.md` (Scope, Files, Approach, Deviations). What changed is in `git diff main...HEAD` and `git diff main...HEAD --stat`. The claims are in `pr_draft.md`.

**What good looks like.**
- Every changed file appears in the plan's Files list, or a deviation note covers it.
- Every hunk does what the plan's approach describes.
- Everything the plan promises is in the diff, or a deviation note defers it.
- Every claim in the description ("exactly as planned", "no other changes", "also documents X") is true of the diff.

**What silent drift looks like.**
- *More than the plan:* the diff adds a new option, flag or setting, a refactor, a rename pass, or edits to a file the plan never names, and the description doesn't say so.
- *Less than the plan:* a promised piece (a docs update, a second fix) is missing and no note says so, or the description claims it is there.

An honest shortfall is not drift. A shortfall named in the plan's deviation note and restated in the description is a scoped PR.

## Test evidence (harness category: not-tested)

**Where it lives.**
- Eval: the proof is in the Candidate PR's Test evidence section, and in any test results quoted in the Description. It is read against the Plan context's test plan and repro evidence. The repo's own test command is in the Repo facts block's pull-requests and contribution-policy lines.
- Live: the proof is in `test_evidence.md` (before and after output, plus `make test-unit`, `make test-integration`, `make lint` and `make typecheck` results). It is read against the Test plan in `plan.md` and the posted repro. The repo's checks are listed in the Testing section of `.github/PULL_REQUEST_TEMPLATE.md`.

**What decisive looks like.**
- The evidence names the command or steps that re-run the plan's repro, and states what came out after the fix next to what came out before. The before result can be cited from the repro.
- Every failure mode the plan's test plan names is re-run, not just one.
- The re-run exercises the changed path, not a control case that never broke.
- Where the repo names a suite command, that command and its outcome appear (for example, "`go test ./...` passes (4108 tests)").

**What it is not.**
- "Tested locally", "works on my machine" or "tests pass" with no command named.
- A suite run with no repro re-run.
- Evidence that exercises an unchanged path.

## Diff quality (harness category: unreviewable)

**Where it lives.**
- Eval: the Candidate PR's Diff, read hunk by hunk. The Commits list adds context, but commit messages alone never decide a grade.
- Live: `git diff main...HEAD`.

**What a reviewable change looks like.** Every added and removed line is part of the fix, its test, or a file entry the repo asks for.

**The debris tells.**
- Debug prints or logging added while debugging (`print`, `eprintln!`, `console.log`, `DEBUG`).
- Commented-out code, including a commented-out first attempt.
- Dead or unused functions, including ones kept alive with `allow(dead_code)` or an `_unused` name.
- Added TODO markers.
- Re-indentation, import reordering, whitespace changes or re-printed identical lines that the fix doesn't need.

## Standards and comms (harness category: standards-wall)

**Where it lives.**
- Eval:
  - The Repo facts block's "pull requests:" line lists the template sections, checklist, required issue link, and required changelog or whatsnew entry.
  - The "contribution policy:" line gives the stated AI policy, or says there is none.
  - The Thread highlights carry the maintainer's explicit questions and asks.
  - The PR's compliance shows in the Title, Description and Diff (for a required file entry).
- Live:
  - Path Review's `.github/PULL_REQUEST_TEMPLATE.md` sections (Summary, Issue, Changes, Testing, Screenshots / Demo, Notes for Reviewers) and `CONTRIBUTING.md`.
  - The `scope.md` house rules: the template is always used, including the disclosure.
  - The issue thread on GitHub.
  - Compliance shows in `pr_draft.md`.

**What compliant looks like.**
- Every section the template names has real content. Judge the content, not the heading format; an inline "Problem:" label counts.
- A required "Closes #N" link is present.
- A required checklist is addressed.
- A required changelog entry is in the diff.
- Where the repo's AI policy asks for disclosure, the description says which AI tool was used and how much it helped.
- Explicit maintainer questions in the thread are answered.

**What a wall looks like.**
- A stated checklist left out entirely.
- A required entry missing from the diff.
- Boilerplate left unfilled.
- A strict AI policy with no disclosure anywhere.

Whether the description's claims match the diff is plan fidelity (above), not this family.
