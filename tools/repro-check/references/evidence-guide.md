# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

Every eval package has the same sections, in this order: a **Repo
facts** block (stars, latest release, a "bug reports: template asks
for..." line, and a "contribution policy" line that states any AI-use
policy), the **Issue** (title, who opened it, body), **Thread
highlights**, the **Candidate claim comment**, and the **Candidate
repro report**.

## Environment

**Where it lives.**
- Eval bundle: the environment lines inside the Candidate repro report
  (operating system, release or version, commit or branch), read
  against any OS, version or platform the Issue section names.
- Live: the draft repro comment, read against the issue body on GitHub.

**What good looks like.** The report names its OS and the code state it
ran (a release, commit or branch), plus every version or platform the
issue names. Where its setup differs from the issue's, such as a newer
release or another OS, the report says so. Fields a repo's bug-report
template asks for beyond these are not required.

## Steps

**Where it lives.**
- Eval bundle: the steps in the Candidate repro report, from the
  starting state it names to the trigger; the Issue body's own steps,
  when the report explicitly points to them.
- Live: the steps in the draft repro comment, and the issue body's
  steps.

**What good looks like.** A stranger starting from the named state
reaches the trigger without guessing. Every command, input and setting
needed is written in the report or explicitly pointed to in the issue,
and any issue steps pointed to are complete themselves. "Set up the
project" or "configure it" with no how is a gap.

## Behavior shown

**Where it lives.**
- Eval bundle: text pasted into the Candidate repro report (command
  output, log lines, error messages, stack traces), read against the
  behavior the Issue section describes.
- Live: the output pasted into the draft repro comment, read against
  the issue body.

**What good looks like.** A pasted artifact shows the issue's own
behavior at its trigger: the same error text or the same symptom, not a
different error nearby. For a cannot-reproduce, the pasted output shows
what happened instead at that trigger. Prose describing what happened,
however specific, is not an artifact, and a screenshot described in
words counts as prose.

## Honesty

**Where it lives.**
- Eval bundle: each factual sentence in the Candidate claim comment and
  the Candidate repro report, set beside the pasted artifact that backs
  it; Thread highlights, for what others have already established.
- Live: the draft comments, and the thread on the issue page.

**What good looks like.** A claim to have reproduced or confirmed the
issue points to a pasted artifact that actually shows the issue's
behavior; "confirmed" next to output showing a different error
overreaches. Generalizations beyond the author's own runs ("it happens
on every machine", "everyone has this") and root causes stated as fact
overreach unless evidence shows them. The author's own account of their
procedure (ran it five times, tried a padded variant, dropped a flag as
a control) is honest reporting, not overreach, as long as one pasted
artifact shows the main result. A root-cause idea labeled as a guess
("this might be...") is honest. A cannot-reproduce that shows its
evidence is honest and passes.

## Comms

**Where it lives.**
- Eval bundle: the repo-facts "contribution policy" line, including any
  AI-use policy; the Candidate claim comment, read against the Issue's
  title and body; Thread highlights, for existing claims.
- Live: the repo's contribution guide (`docs/CONTRIBUTING.md` on Path
  Review), any `AI_POLICY.md` or `AGENTS.md`, the issue templates under
  `.github/ISSUE_TEMPLATE/`, and the house rules in `scope.md`; the
  draft claim comment against the issue.

**What good looks like.** The claim names something only this issue has
(a file, variable, error or behavior) and says what its author will do
next. If the policy requires AI disclosure, at least one comment in the
package discloses it; an outright ban on AI contributions is a fail; no
stated policy is a pass. Under Path Review's house rules, a classmate's
claim on the same issue does not block a new claim.
