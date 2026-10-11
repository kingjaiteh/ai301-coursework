# Procedure: how this tool grades a PR package

## Read order

1. **Repo facts first.** Write down the following before reading the PR, so the PR's own framing can't set the standard:
   - every PR ask the repo states: template sections, checklist, required issue link, required changelog or whatsnew entry, test or check commands;
   - the AI policy, written down word for word, or "none stated".
2. **Issue and thread highlights.** Write down the problem in one line, and every explicit maintainer question, ask or warning.
3. **Plan context.** Read it before the PR, because every side-by-side check measures the PR against it. Write down:
   - the Files list;
   - what is in scope and what is not;
   - each change the approach promises;
   - each failure mode the test plan names, with its expected after;
   - any deviation or deferral note.
4. **Diff, before the description.** List every changed file from its `+++ b/` line. For each hunk, note what it does, or note that it is debris. Reading the diff before the description keeps a confident description from shaping what you see.
5. **Description and title.** List each factual claim about what changed, what was left alone, and what was tested.
6. **Test evidence.** For each failure mode from step 3, record the command that re-ran it and the after result. Record every suite or check command named, with its outcome.
7. **Commits.** Read them for context only.

In live mode, steps 1 to 7 read the live sources listed in SKILL.md, not bundle sections.

## Evidence gathering

Use `references/evidence-guide.md` for where each item lives.

- **plan-fidelity.** Pair each changed file (step 4) with the plan's Files list or a deviation note. Pair each promised change (step 3) with the hunk that delivers it or the note that defers it. Record any unpaired file, hunk or promise.
- **description-fidelity.** Pair each claim (step 5) with the hunk that makes it true. Record any claim the diff contradicts or doesn't contain.
- **decisive-evidence.** Pair each failure mode the test plan names (step 3) with its re-run (step 6). Record any failure mode with no re-run, and any re-run that exercises a control or unchanged path. Pair each repo-named test command (step 1) with a named run and its outcome.
- **clean-diff.** Record each debris line from step 4, with its file and the kind of debris.
- **template-followed.** Pair each stated PR ask (step 1) with where the PR meets it: a description section, a "Closes #" line, a checklist, or a diff entry. Record any unmet required ask.
- **ai-disclosure.** Pair the AI policy (step 1) with the disclosure sentence in the description, if one exists. Record whether the disclosure meets what the policy asks.
- **thread-engaged.** Pair each maintainer ask (step 2) with where the plan or description addresses it.

## Check execution

1. Run the checks in rubric order: plan-fidelity, description-fidelity, decisive-evidence, clean-diff, template-followed, ai-disclosure, thread-engaged.
2. Grade each check only from its gathered pairings and the pass condition in `rubric.md`. Don't re-read the whole package unless a pairing is missing.
3. Grade `pass` when the pass condition is met, and `fail` when the evidence shows it isn't.
4. Grade `unclear` when the evidence the check needs is absent from the package. For example, the test evidence section is empty, or the diff is truncated where a claim needs it. Don't infer missing evidence from a confident description.
5. Every grade gets a one-line evidence string. For a pass, it is the fact or quote that decided it. For a fail or unclear, it is the first unpaired item, quoted or named with its file.
6. If this procedure doesn't say how to gather or grade something a check needs, report the gap in the summary and grade the check `unclear`. Don't improvise a new step.

## Verdict assembly

1. Apply the verdict rule in `rubric.md`: accept only if every required check is `pass`. An `unclear` grade on a required check counts as a fail. Preferred checks never change the verdict.
2. The deciding check is the first required check in rubric order that is not `pass`. On an accept there is no deciding check.
3. In the summary before the JSON block, name the deciding check and quote its evidence line. List any other failing checks after it.
4. Emit every check in rubric order in the JSON `checks` array, preferred ones included. Then emit the verdict. The same grades always produce the same verdict.
