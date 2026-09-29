# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| claim-specific | The candidate claim comment, read against the issue's title and body | The claim names at least one detail only this issue has (a file, variable, error message, command or behavior taken from the issue) and states the next action its author will take. A claim that could be pasted onto any issue ("+1", "claiming this", "I'll look into it") fails | required |
| policy-respected | The repo-facts "contribution policy" line, including any AI-use policy, read against the candidate claim comment and repro report together | If the policy requires disclosing AI assistance, at least one of the two comments discloses it. If the policy bans AI-generated contributions, fail. If the policy states no AI rule, pass. In a claim-only draft, the claim comment alone must satisfy this | required |
| env-recorded | The repro report's environment record, read against the OS, versions and platform the issue itself names | The report names its operating system, the version or code state (a release, commit or branch) of the software it ran, and every version or platform the issue names. Where the report's setup differs from the issue's, the difference is stated. Fields a repo's bug-report template asks for beyond these are not required | required |
| steps-rerunnable | The repro report's steps, from the starting state it names through the trigger, plus the issue body's own steps where the report explicitly points to them | A stranger starting from the stated state could reach the trigger using only the report and any issue steps it points to, provided those issue steps are complete themselves. Every command, input or setting needed is written or pointed to; no step like "set up the project" or "configure it" is left without saying how | required |
| shows-issue-behavior | The artifacts pasted into the repro report (command output, log lines, error text, stack traces), read against the behavior the issue describes | At least one pasted artifact shows the behavior the issue describes at the issue's trigger: the same error or the same symptom, not a neighbouring one. For a cannot-reproduce, a pasted artifact shows what happened at that trigger instead. Prose describing what happened, however specific, does not count as an artifact | required |
| claims-backed | Every factual claim in the candidate claim comment and repro report, set beside the pasted artifact that backs it | No claim reaches past its evidence. A claim to have reproduced or confirmed the issue is backed only when a pasted artifact shows the issue's own behavior. Claims that generalize beyond the author's own runs ("every machine", "everyone", "all versions") or state a root cause as fact fail unless a pasted artifact shows them. The author's first-person account of their own procedure (how many times they ran it, variations and control runs they tried, what they changed between attempts) does not need a separate artifact per sentence, provided at least one pasted artifact shows the main result. A root-cause idea explicitly labeled as a guess or hypothesis passes. A cannot-reproduce stated with its evidence passes | required |

## Verdict rule

Accept if every required check passes. This rubric has no preferred
checks.

Unclear counts as fail on every check, because proof that cannot be
verified is not ready to post. One exception: policy-respected passes
when the repo facts state no AI-use policy at all, because a repo's
silence is not a restriction.

In a claim-only draft, only claim-specific and policy-respected are
graded. The other four are reported as not yet applicable and are left
out of the verdict.
