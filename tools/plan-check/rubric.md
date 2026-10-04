# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The candidate plan's stated cause, read against every observation in the Repro evidence section, including control steps that change one condition at a time | The stated cause explains every behavior the repro evidence reports, including what changes and what stays the same across its control steps, and the plan's change targets that cause rather than only the symptom. A cause the repro evidence rules out fails, and so does a plan that puts the evidenced cause out of scope. Agreement with the issue report or a thread comment alone is not enough | required |
| scope | The Issue section, and the candidate plan's scope statement: its in-scope and out-of-scope lines and the files or areas it names | The change to code or docs is limited to what the issue and its diagnosed cause need. Refactors, renames, unrelated fixes or new features fail unless the plan explicitly puts them out of scope. Extra tests or manual checks do not count against scope | required |
| executable | The candidate plan's change description: the files, functions or areas it names, and the concrete edit at each | A stranger could start the change without asking the author anything: the plan names where the change goes (a file, function or clearly identified area) and what changes there. A goal with no location or no concrete edit ("improve the handling", "make it faster") fails | required |
| test | The candidate plan's test plan, read against the Repro evidence's steps and expected result | The test re-runs the reproduction, or a check that runs through the real code, and names an observable result that would be different if the fix had failed. A test that would already pass before the fix, or "run the tests" with no expected result, fails | required |
| thread-aware | The candidate plan comment, read against Thread highlights and the repo-facts contribution policy line | The comment does not contradict a maintainer's stated ask, approach or warning in the thread; follows conventions the repo facts actually state (such as review bandwidth, approval before a pull request, or AI disclosure); and does not present another commenter's unverified claim as settled. Conventions not stated in the thread or repo facts are not grounds to fail | required |
| unknowns-honest | Certainty claims in the candidate plan and comment, set beside what the repro evidence supports | No claim of certainty beyond the evidence ("definitely fixes it", "the only cause"), and open questions are stated as open | preferred |

## Verdict rule

Accept if every required check passes. unknowns-honest is preferred and
never changes the verdict.

Unclear counts as fail on diagnosis, scope, executable and test, because
a plan's cause, bounds, location and test all have to be in the plan
itself: if they cannot be found there, the plan is not ready.

Unclear counts as pass on thread-aware when the thread highlights and
the repo facts state no maintainer ask, approach, warning or convention
that bears on the comment, because a convention nobody stated cannot be
broken.
