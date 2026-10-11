---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question about one PR package: **is this pull request ready to submit?**

A PR package has five parts: the candidate PR's title, its description, its commits, its diff and its test evidence. Read the package against two things: the plan it claims to implement (including the plan's deviation notes), and the issue that plan belongs to, together with the repo's stated standards.

Grade exactly one package per run. Don't review code style, suggest a different fix, or answer any other question about the issue or the repo.

## Inputs and modes

Decide the mode first. If the prompt supplies an eval package bundle (a "# Eval package" document with Repo facts, Issue, Plan context and Candidate PR sections), use **eval mode**. Otherwise use **live mode**.

**Live mode** grades the student's own PR before it is opened. Read these inputs from the working copy, which is the top folder of the student's fork clone:

- **The plan:** `plan.md`, including its Deviations section. A house-chain student reads the house plan and the house repro pack the instructor routed them to instead.
- **The diff:** everything the branch changes relative to the repo's default branch. Produce it by running `git diff main...HEAD` (three dots) and `git diff main...HEAD --stat` from the working copy. The commits come from `git log main..HEAD --oneline`.
- **The draft title and description:** `pr_draft.md`.
- **The test evidence:** `test_evidence.md`.
- **The issue:** the issue URL the student gives. On GitHub, read the issue body and its thread.
- **The repo's stated standards:** `.github/PULL_REQUEST_TEMPLATE.md` and `CONTRIBUTING.md` in the working copy, plus the house rules in `scope.md`.

If any input is missing, say which one. Then grade the checks that depend on it `unclear`; don't skip them.

**Eval mode:** the bundle is the whole world. Every fact comes from the bundle text. Fetch nothing, run no commands, and read no file other than this tool's components. Always grade the complete package: every check in `rubric.md`, under the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else.

1. If its `Repo:` line still holds the placeholder `<ORG>/<PATH-REVIEW-REPO>`, stop without grading. Tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo.
2. If the PR would target any repository other than the one named on the `Repo:` line, refuse to grade, and say which repo is in scope. Never guess a scope.
3. Apply the house rules `scope.md` lists as part of the standards evidence. These are: the PR comes from a `fix/<issue-number>-<slug>` branch on the student's fork, there is one PR per issue per student, and the template is always used, including its disclosure. A classmate's PR on the same issue never counts against the student.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after grading, read `voice-guide.md`. Hold the outgoing PR text (the title and description in `pr_draft.md`) against each rule and each "never post" item. In the summary, list every rule the draft breaks, quoting the offending phrase and naming the rule. If no rule is broken, say so in one line.

Voice findings never change the verdict: no rubric check reads the voice guide, and voice is personal. They go in the summary only, not in the JSON checks.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Before grading, read these components from this tool's directory:

- `rubric.md` defines the checks, their pass conditions and the verdict rule. Grade only the checks it defines, by its stated conditions. Never invent or drop a check.
- `references/evidence-guide.md` maps where each evidence family lives, in a bundle and in live mode, and what good looks like.
- `procedure.md` is the operating steps: read order, evidence gathering, check execution and verdict assembly. Execute it as written, in order.

When the procedure is silent on a step a check needs, report the gap in the summary and grade that check `unclear`. Never improvise around a gap.

If `rubric.md` has no filled checks table or no verdict rule, or `procedure.md` has no written steps, refuse to grade: say which component is empty and that the tool will not produce a verdict without it. Instruction comments and empty template rows do not count as content.

## Verdict and output

The verdict is binary:

- `accept` means ready to submit.
- `reject` means hold.

There is no third verdict and no score. Reservations go in a check's evidence line, never in the verdict.

Start the reply with a short readable summary:

- each check's grade and its evidence line;
- the deciding check, as `procedure.md` defines it;
- in live mode, the voice findings and any input gaps.

Then end the reply with this fenced JSON block. It must be valid, it must be last, and nothing may follow it. Put the PR URL (live) or bundle id (eval) in `item`. List every rubric check in rubric order.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first.** Grade no check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- **Grade the thing, not the polish.** A terse but complete PR can be ready. A polished, confident description can hide drift. Read the diff and the commands' output against the plan, the issue and the stated standards, never the formatting or the tone.
- **The rubric decides, not the run.** If a check passes by its stated condition but feels wrong, grade it pass and note the doubt in the summary. The fix belongs in `rubric.md`.
- **The procedure decides how.** Follow `procedure.md` as written, and report its gaps instead of inventing steps.
- **Unclear counts as fail.** The verdict rule treats `unclear` as fail on every check. Where any rule is silent, a claim you cannot verify from the package is a failing one: a PR you cannot verify is not ready to submit.
- **Honest outcomes can pass.** A PR that openly discloses a shortfall in its plan notes and description can be ready. "Less than everything" is not by itself a hold.
