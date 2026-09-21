# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

**Verdict output**

```
All three URLs are inside the scoped repo (codepath/pathreview-ai301-fa26-s1), so all three are valid candidates. One note before the grades: the fit profile in scope.md is still the placeholder — "(Write a few sentences here.)" So I ranked the accepted issues by the rubric's preferred checks rather than by your fit. Filling that section in will change the ordering, not the verdicts.

## Repo-level evidence (shared by all three)

| Check | Grade | Evidence |
|---|---|---|
| maintainer-alive | pass | All 5 latest main commits (3x 2026-09-16, 2x 2026-08-24) fall within 30 days of today (2026-09-20); all authored by Aburke225, a human COLLABORATOR |
| repo-in-use | pass | isArchived: false; no releases, but last push 2026-09-16 — 4 days ago, well inside 90 |
| ai-policy-ok | pass | No CONTRIBUTING.md at root/.github, no AI_POLICY.md/AGENTS.md; docs/CONTRIBUTING.md has zero AI/assistant/LLM-policy language and the PR template has no AI-disclosure box — silence passes |
| issue-response-latency (preferred) | fail | Of the 5 most recently updated issues (68, 69, 73, 52, 43), only 2 drew a COLLABORATOR reply; #68 and #69 have student comments sitting unanswered |

## Ranked read-out — all three accept

1. #73 — README and .env.example disagree about which LLM API key to set
Cleanest of the three on preferred checks: the only candidate that passes low-setup. The work is README.md + .env.example, two files you can fix and verify by reading core/config.py — no docker stack, no venv, no test run. Two deliverables, zero comments, zero claims, maintainer-opened with good first issue + tier-1.

2. #62 — Health check references settings.redis_host, which does not exist on Settings
Tightest actual code fix: one line in api/routes/health.py swapping the nonexistent settings.redis_host/redis_port for the real redis_url. Completely untouched — no comments, no claims, no linked PR. Costs you low-setup, since reproducing the 503 means running the API against a live Redis.

3. #68 — Keyword search raises ZeroDivisionError when the index is empty
Still an accept, but last. yulijasso (author_association NONE — a classmate, not a maintainer) has posted a detailed claim plus a full reproduction. Under the Path Review house rule that does not block the issue and unclaimed passes; it just means your PR would land beside a well-developed one. It also carries the largest scope of the three: a guard in rag/retriever/keyword_search.py, plus removing the xfail marker and any matching pyproject.toml suppression, at a stated 2-4 hours.

No candidate failed a required check, so nothing was rejected.
```

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "All 5 latest main commits (2026-09-16 x3, 2026-08-24 x2) are within 30 days of 2026-09-20 and authored by human collaborator Aburke225"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived=false; no releases but last push to any branch 2026-09-16, 4 days before capture"},
      {"name": "ai-policy-ok", "grade": "pass", "evidence": "No CONTRIBUTING.md at root/.github, no AI_POLICY.md/AGENTS.md; docs/CONTRIBUTING.md and the PR template state nothing about AI use"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; timeline shows no connected or cross-referenced PRs; comment count 0"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Maintainer-opened single-defect issue labeled 'good first issue'/'tier-1'; no umbrella list, no design debate, no core-internals statement, not a support question"},
      {"name": "target-named", "grade": "pass", "evidence": "Body lists 'Relevant files: README.md, .env.example' and cites core/config.py as the source of truth"},
      {"name": "issue-response-latency", "grade": "fail", "evidence": "Only 2 of the 5 most recently updated issues (52, 43) drew a COLLABORATOR reply; #68, #69 and #73 have none"},
      {"name": "low-setup", "grade": "pass", "evidence": "Work is confined to README.md and .env.example, verifiable by reading core/config.py without running the project"},
      {"name": "bounded-deliverables", "grade": "pass", "evidence": "Two deliverables (add OPENROUTER_API_KEY to .env.example, correct the LLM_PROVIDER comment); no new dependency, schema or public API"},
      {"name": "stack-familiar", "grade": "pass", "evidence": "Prose/docs plus a dotenv config file in a Python + React/TypeScript repo"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "All 5 latest main commits (2026-09-16 x3, 2026-08-24 x2) are within 30 days of 2026-09-20 and authored by human collaborator Aburke225"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived=false; no releases but last push to any branch 2026-09-16, 4 days before capture"},
      {"name": "ai-policy-ok", "grade": "pass", "evidence": "No CONTRIBUTING.md at root/.github, no AI_POLICY.md/AGENTS.md; docs/CONTRIBUTING.md and the PR template state nothing about AI use"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; timeline shows no connected or cross-referenced PRs; comment count 0"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Single defect in api/routes/health.py with reproduction steps; no umbrella list, no design debate, no core-internals statement, not a support question"},
      {"name": "target-named", "grade": "pass", "evidence": "Body names api/routes/health.py, the Settings class in core/config.py, and the GET /health endpoint"},
      {"name": "issue-response-latency", "grade": "fail", "evidence": "Only 2 of the 5 most recently updated issues (52, 43) drew a COLLABORATOR reply; #68, #69 and #73 have none"},
      {"name": "low-setup", "grade": "fail", "evidence": "Fix is application code in api/routes/health.py and the stated repro requires calling GET /health against a running Redis"},
      {"name": "bounded-deliverables", "grade": "pass", "evidence": "One deliverable (point the probe at settings.redis_url); no new dependency, schema or public API"},
      {"name": "stack-familiar", "grade": "pass", "evidence": "Python (FastAPI route plus pydantic Settings)"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "All 5 latest main commits (2026-09-16 x3, 2026-08-24 x2) are within 30 days of 2026-09-20 and authored by human collaborator Aburke225"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived=false; no releases but last push to any branch 2026-09-16, 4 days before capture"},
      {"name": "ai-policy-ok", "grade": "pass", "evidence": "No CONTRIBUTING.md at root/.github, no AI_POLICY.md/AGENTS.md; docs/CONTRIBUTING.md and the PR template state nothing about AI use"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; no linked PRs in the timeline; the two claim comments are from yulijasso (author_association NONE, a classmate), which the Path Review house rule says does not block"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "One empty-corpus guard in KeywordSearcher.index() plus removing the xfail marker; no umbrella list, no design debate, no core-internals statement, not a support question"},
      {"name": "target-named", "grade": "pass", "evidence": "Body lists 'Relevant files: rag/retriever/keyword_search.py, tests/unit/test_keyword_search.py' and names KeywordSearcher.index()"},
      {"name": "issue-response-latency", "grade": "fail", "evidence": "Only 2 of the 5 most recently updated issues (52, 43) drew a COLLABORATOR reply; this issue's own two comments are unanswered after 0 days but no maintainer has replied"},
      {"name": "low-setup", "grade": "fail", "evidence": "Fix edits source in rag/retriever/keyword_search.py and verification requires the project installed locally to run make test-unit with rank-bm25"},
      {"name": "bounded-deliverables", "grade": "pass", "evidence": "Two deliverables (empty-corpus guard, remove the xfail marker and any pyproject suppression); no new dependency, schema or public API"},
      {"name": "stack-familiar", "grade": "pass", "evidence": "Python source plus a pytest unit test"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

**Run history**

Run 1 — `--only issue-01`, first rubric: agreement 0/1.

Run 2 — `--only issue-01`, after revising the rubric: agreement 1/1.

Run 3 — first full run: no agreement score, crashed partway with
`UnicodeEncodeError: 'charmap' codec can't encode character '✨'`.

Run 4 — full run with `python -X utf8`: agreement 18/20, bar PASS. This is the run
saved to `eval-run.txt`.

**Issue analysis**

`issue-01` (conda/conda#16475, captured 2026-08-05). My rubric's decision: `reject`.
Gold label: `accept`.

The evidence in the bundle:

- last 5 default-branch commits all dated 2026-08-04, one day before capture, by two
  non-bot authors
- maintainer first-response sample: 4 of 5 recent threads drew no maintainer reply,
  the fifth took 32.9 days
- the issue itself has 0 comments and names `manage-pkgs.rst`,
  `pip-interoperability.rst`, `new-features.md` and `troubleshooting.rst`

Three required checks failed, and each read the bundle differently than I intended.

maintainerresponsive: The check evaluated whether maintainers replied to recent issue
threads. It failed here because 4 of the 5 recent threads received no response, and
the fifth took nearly 33 days.Instead of relying on issue thread replies, the check should have evaluated the repository's commit velocity—specifically the five default-branch commits dated August 4, 2026, just one day prior to capture.

acceptance-stated:
The check required that the definition of done be expressible in one sentence using the issue's own words, with no maintainer decision still outstanding. Because the issue had zero comments, no maintainer had weighed in, which automatically prevented that second condition from ever being satisfied.

scope-bounded: The check required the change be confined to at most two named files.
It marked the issue as unbounded because it references four separate doc files
(`manage-pkgs.rst`, `pip-interoperability.rst`, `new-features.md` and
`troubleshooting.rst`), plus a new page to create. However, the task itself is a
straightforward documentation sync that doesn't involve complex code changes across
those files.

**Check rationale**

Quote, from `maintainer-alive` as currently written in the uploaded `rubric.md`:

> Evidence: repo-facts block: the "last 5 default-branch commits" list, both dates
> and author names
>
> Pass condition: At least 3 of the 5 commits are dated within 30 days of the capture
> date and are authored by non-bot accounts (a username ending in `[bot]` counts only
> if the commit merges a human's PR)

I designed this check to prioritize recent commit activity over issue comments
because commit velocity is a more reliable indicator of active maintenance. Looking
at the last 5 default-branch commits rather than all of them provides a focused
snapshot of recent activity without letting outdated commits skew the metric. I set
the threshold to 3 out of 5 commits within 30 days to allow for natural lulls in
maintenance while still ensuring regular updates. Finally, I added the bot clause to
ensure that automated dependency updates or bot-generated commits aren't mistaken for
genuine human maintenance.

**Trade-offs**

I accept the trade-off inherent in `maintainer-alive`: it will occasionally
misclassify repos that merge code steadily but rarely respond to issue threads. Path
Review is a clear example of this — the live run failed `issue-response-latency`
because only 2 out of 5 recently updated issues received a collaborator reply, even
though active development was still taking place.

---

## Selection rationale

Issue #73 fits well into my schedule around my weekday job. Since the changes are
confined to just two files, README.md and .env.example, which I verified by
inspecting core/config.py, it will only require one or two evenings of work to
complete.

The rubric correctly flagged #73 as a top candidate due to its minimal setup
requirements and clearly bounded deliverables. However, the automated grading
couldn't account for personal preference and context: while I would typically prefer
a Python coding task for my portfolio over documentation fixes, #68 already has a
detailed claim from a classmate, making #73 the best available choice.

Claiming #73 should be straightforward because it was opened by a maintainer,
currently has zero comments, no assignee, and no linked pull requests. The main
obstacle will be maintainer responsiveness, as the repository resolves issues slowly:
only 2 out of the 5 recent issues received a response from a collaborator.
