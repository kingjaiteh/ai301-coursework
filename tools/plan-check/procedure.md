# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the Repo facts block first. Write down the contribution policy line word for word, any AI-use or disclosure rule, and any stated ask about pull requests or reviews.
2. Read the Issue. Write down the behavior it reports, the trigger, and any version or platform it names.
3. Read the Thread highlights. For each comment, write down the author, their association (OWNER, MEMBER, COLLABORATOR or NONE), and any ask, approach, warning or root-cause claim it makes. Mark which claims come from maintainers and which do not.
4. Read the Repro evidence before the plan. Write down every observation it reports, step by step, including control steps that change one condition (a flag, a setting, an input) and what changed or stayed the same as a result. This list is what the plan's cause must explain.
5. Read the Candidate plan, then the Candidate plan comment, last. Reading the evidence first means the plan's own framing cannot set what counts as the evidence.

## Evidence gathering

1. For diagnosis: quote the plan's stated cause. Next to it, list each repro observation from read-order step 4, and mark whether the cause explains it. Also note whether the plan puts any evidenced cause out of scope.
2. For scope: quote the plan's in-scope and out-of-scope lines and list every file, area or change it names. Mark each change as needed by the issue and its cause, or extra. Do not count tests or manual checks as changes.
3. For executable: list each change the plan describes, with the location it names (file, function or clearly identified area) and the concrete edit at that location. Mark any change that has no location or no concrete edit.
4. For test: quote the plan's test plan. Name which repro step it re-runs, or which real-code check it runs, and the observable result it expects. Then ask whether that result would already be true before the fix.
5. For thread-aware: from read-order steps 1 and 3, list each maintainer ask, approach or warning and each stated repo convention. For each, quote the comment's sentence that meets or breaks it, or note that the comment does not touch it. Also note any non-maintainer claim the comment presents as settled.
6. For unknowns-honest: quote every certainty word in the plan and comment ("definitely", "will fix", "the only cause") and set it beside the evidence for it.

## Check execution

1. Run the checks in the rubric's table order: diagnosis, scope, executable, test, thread-aware, unknowns-honest.
2. Grade each check only from the evidence gathered for it in the previous stage. Re-read the package only if that evidence is missing from the notes.
3. Grade pass or fail by the rubric's pass condition, word for word. Do not add conditions the rubric does not state.
4. Grade unclear only when the evidence the check needs is genuinely absent from the package, never because a call is hard. Write which evidence is missing.
5. Every grade cites one quote or fact from the gathered evidence that decided it.

## Verdict assembly

1. Treat unclear grades exactly as the rubric's verdict rule says: unclear is a fail on diagnosis, scope, executable and test; on thread-aware it is a pass when no stated ask or convention bears on the comment.
2. Ignore the preferred check (unknowns-honest) when deciding; report its grade but never let it change the verdict.
3. If every required check passes after step 1, the verdict is accept. Otherwise it is reject.
4. In the summary, name the check that decided a reject and quote the evidence that failed it. If several failed, name each.
5. End with the JSON block in the format SKILL.md requires.
