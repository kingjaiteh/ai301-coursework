# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where it lives.** Eval: the cause statement in the Candidate plan (often under Cause or Diagnosis), read against every step in the Repro evidence section, including its control steps and its expected and actual results. Live: the diagnosis in your plan.md, read against your posted Unit 2 repro comment, as quoted in the plan.

**What good looks like.** The stated cause explains every reproduced observation, including what changes when a control step changes one condition. A cause that only matches the issue report or a thread comment, while a repro step rules it out, is a wrong cause. So is a plan that names the evidenced cause and then puts it out of scope.

## Scope

**Where it lives.** Eval: the Candidate plan's change description and its In and Out (or in-scope and not-in-scope) lines, and the files or areas it names, read against the Issue section. Live: the scope and files sections of your plan.md.

**What good looks like.** One bounded change that the issue and its cause need, with anything nearby explicitly put out of scope. Refactors, renames, unrelated fixes or features riding along are scope creep. Extra tests or manual checks are not.

## Executability

**Where it lives.** Eval: the Candidate plan's change or approach section: file paths, functions, callbacks, settings, and the edit at each. Live: the approach and files sections of your plan.md.

**What good looks like.** A stranger could open the named file, function or clearly identified area and start the edit without asking. "Improve the handling" or "make it faster" with no location or no concrete edit cannot be started.

## Test plan

**Where it lives.** Eval: the Candidate plan's test line or section, read against the Repro evidence steps and expected result. Live: the test plan in your plan.md, against your Unit 2 repro steps.

**What good looks like.** The test re-runs the reproduction, or a check through the real code, and names an observable result that would be different if the fix failed. A test that would already pass before the fix, or "run the tests" with no expected result, proves nothing.

## Honesty

**Where it lives.** Eval: certainty words in the Candidate plan and plan comment ("definitely", "will fix", "the only cause"), and any risks or unknowns the plan states. Live: the risks and unknowns section of your plan.md, and its Deviations section after the build.

**What good looks like.** Claims stay within what the repro evidence supports, and open questions are stated as open. A deviation recorded honestly after the build is good evidence, not a failure.

## Comms

**Where it lives.** Eval: the Candidate plan comment, read against Thread highlights (each comment's author association and any ask, approach or warning) and the repo-facts contribution policy line. Live: your comment.md, against the live issue thread, including any linked pull requests, and the repo's docs/CONTRIBUTING.md.

**What good looks like.** The comment is consistent with what maintainers said in the thread and with conventions the repo facts actually state, such as review bandwidth, approval before a pull request, or AI disclosure. It does not present a non-maintainer's unverified root-cause claim as settled, and it is its own plan rather than "same approach as above." Conventions nobody stated are not grounds to fail.
