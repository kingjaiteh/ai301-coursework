# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

---

## Posted upstream

**GitHub username**

kingjaiteh

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5984167810

The README and docs/SETUP.md both tell users to set `OPENROUTER_API_KEY`, but `.env.example` omits it entirely while listing only mock and openai in the LLM provider comment (from my repro above, https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5900274210). I plan to add `OPENROUTER_API_KEY` to `.env.example` under the existing `OPENAI_API_KEY` line, and leave the `LLM_PROVIDER` comment and the rest of the template unchanged. I can verify the fix by running `grep -c "OPENROUTER_API_KEY" .env` on a fresh copy after `cp .env.example .env`; it should print `1` instead of the current `0`.

I see PR #77 also edits `.env.example` and `README.md`. That PR documents an `LLM_PROVIDER=openrouter` option; this fix just adds the environment variable to the template. I'm not adding "openrouter" to the `LLM_PROVIDER` comment because nothing in the code reads `LLM_PROVIDER`, so I can't verify that value does anything. Keeping this change narrower than #77 makes each PR clearer about what it does.

The issue names two mismatches: the missing key and the comment that offers only mock and openai. This fix covers the first; the second stays unchanged. Would you want the `LLM_PROVIDER` comment updated to list openrouter as well, or does that depend on how PR #77 resolves?

---

## Your branch

**Branch**

fix/73-env-example-openrouter-key

**Evidence**

**Before the fix** (from my posted Unit 2 repro, fresh clone of my fork at `f89c06f`, Windows 10, Git Bash):

```
$ cp .env.example .env
$ grep -c "OPENROUTER_API_KEY" .env
0
$ grep -n -A3 "# LLM provider" .env
16:# LLM provider
17-# Options: "mock" (default, no API key needed), "openai"
18-LLM_PROVIDER=mock
19-OPENAI_API_KEY=sk-your-key-here
```

**After the fix** (branch `fix/73-env-example-openrouter-key`, commit `baf6de4`, same machine):

```
$ rm -f .env && cp .env.example .env
$ grep -c "OPENROUTER_API_KEY" .env
1
$ grep -n -A4 "# LLM provider" .env
16:# LLM provider
17-# Options: "mock" (default, no API key needed), "openai"
18-LLM_PROVIDER=mock
19-OPENAI_API_KEY=sk-your-key-here
20-OPENROUTER_API_KEY=sk-or-your-key-here
```

**The change** (`git diff` before commit):

```
--- a/.env.example
+++ b/.env.example
@@ -17,6 +17,7 @@ VECTOR_DB_URL=http://localhost:8001
 # Options: "mock" (default, no API key needed), "openai"
 LLM_PROVIDER=mock
 OPENAI_API_KEY=sk-your-key-here
+OPENROUTER_API_KEY=sk-or-your-key-here
 
 # App settings
 APP_ENV=development
```

---

## Eval iterations

**Run history**

Single run: 19/20 agreement, matching the `eval-run.txt` final score. One disagreement: pkg-20, gold `reject`, graded `accept`.

**Package analysis**

pkg-20 (ghostty-org/ghostty#11261). My rubric returned `accept`; the gold label is `reject`; they disagree. The gold note is "excellent bounded plan that follows the thread's direction, but the comment contains no AI-use disclosure and ghostty's stated policy requires disclosing all AI usage; every package here is treated as AI-assisted work." The plan itself is strong: it aligns perfectly with the thread's proposed direction and shows understanding of the codebase. However, ghostty's stated AI policy requires disclosure of all AI usage, stating the tool and the extent. The plan comment never discloses. `Thread-aware` saw a comment that followed the thread's conventions flawlessly, so it passed. But disclosure sits in my rubric as one example in a parenthetical list of conventions, rather than as a hard requirement, so the missing disclosure didn't cause a failure.

**Check rationale**

Quote the `thread-aware` check from `tools/plan-check/rubric.md`:

"The comment does not contradict a maintainer's stated ask, approach or warning in the thread; follows conventions the repo facts actually state (such as review bandwidth, approval before a pull request, or AI disclosure); and does not present another commenter's unverified claim as settled. Conventions not stated in the thread or repo facts are not grounds to fail".

This check reads that way because the thread and the repo facts are the ground truth for what's actually required. If a maintainer asked for something specific in the issue, the plan comment can't ignore it. If the repo facts state a convention (like "disclosure required"), the plan must follow it. But conventions that aren't actually stated anywhere can't be held against a plan—no hidden standards. The clause about unverified claims is there because one test case (calib-03) showed a comment confidently restating another person's diagnostic guess as settled fact, which would mislead the maintainer about what's actually known. That's different from a difference of opinion or a stated uncertainty.

**Trade-offs**

The `thread-aware` check folds AI disclosure into a parenthetical list of example conventions ("such as review bandwidth, approval before a pull request, or AI disclosure"). On pkg-20, the plan comment follows the thread's proposed direction exactly, so the check sees it as aligned with the thread and holding the stated conventions. But disclosure is buried in the examples, not elevated as a hard boundary, and there is no separate disclosure check in the rubric to catch it. Ghostty's stated policy requires disclosure, but the comment doesn't disclose. The trade-off is that `thread-aware` stays broad and judges only stated conventions, which covers a lot of ground, but disclosure got one mention in a parenthetical and no check of its own. That meant one strong plan that matched the thread perfectly slipped through on a policy violation.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in `tools/plan-check/`.
