# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/132

**Branch**

fix/73-env-example-openrouter-key

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

First run (partial, `--only pkg-20,calib-03 --include-calibration`): smoke test of the first draft. pkg-20 agreed at reject, calib-03 agreed (unscored). No bar verdict on partial runs.

Second run (full, `--save-run eval-run.txt`): 18/20 agreement, meeting the 18/20 pass bar. Categories: clear-accept 5/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3. No changes to any of the four skill files between runs. This is the final run recorded in `eval-run.txt`.

**Package analysis**

pkg-05 (nushell/nushell#18848). My rubric returned `reject` (failed: decisive-evidence); gold label is `accept` (clear-accept). The plan's test section names two failure modes: first, re-run the issue's script and expect both `atuin` rows in the output; second, re-run with two same-name, same-key bindings and expect one row plus a warning. The evidence shows the first mode as a complete before/after table with commands and output. The second mode appears only as a sentence: "Same-key redefine prints the one-time warning." It names no command and shows no output. My decisive-evidence check requires that for every failure mode a plan names, "the evidence names the command or steps that re-run it and states the observed result after the fix". Mode (2) has neither, so it failed. This follows the same rule that holds calib-04 (gold reject): if a plan names a mode, the evidence must demonstrate it.

**Check rationale**

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| ai-disclosure | The repo-facts block's contribution policy (any stated AI policy), read against the PR description. Treat every package as AI-assisted work. | If the repo's stated policy requires disclosing AI use, the description contains a disclosure meeting what the policy asks (for example, the tool used and the extent of assistance). If the policy requires human-written text, the disclosure states the human wrote or reviewed it. If the repo states no AI policy, it passes. | required |

This check reads this way because Unit 3 showed a gap: disclosure appeared only as a parenthetical example inside the thread-aware check, and a plan comment that followed every other thread convention but had no AI disclosure was accepted, though the gold label rejected it. For Unit 4, I separated disclosure into its own required check so that repos with stated AI policies get an explicit test. The clause "if the repo states no AI policy, it passes" keeps the check from failing the clear-accepts whose repos don't have policies—they shouldn't be penalized for a rule that doesn't apply. The result is standards-wall 2/2: pkg-20 (ghostty, whose policy requires disclosing all AI use) is held on this check, while pkg-01 (pandas, no AI policy) passes it and is held on template-followed instead, so the two standards checks each catch a different wall.

**Trade-offs**

decisive-evidence's "every failure mode" rule costs pkg-05. The plan names two failure modes but demonstrates only one with commands and output; the second appears as a sentence only. Gold accepts this as clear-accept, but the rule holds that every named mode must be shown in evidence. I set this rule to match calib-04 (gold reject), where a plan names two modes but re-runs only one, and holding that case meant also holding pkg-05. That's the trade-off I accepted: losing a clear-accept to keep the calib-04 boundary consistent.