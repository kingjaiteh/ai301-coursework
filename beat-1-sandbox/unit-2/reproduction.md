# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

kingjaiteh

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5881349506

The README's Quick Start says it needs to set OPENROUTER_API_KEY, but .env.example doesn't list it; instead, it only shows LLM_PROVIDER with mock and openai as comment options. I'm going to clone a fresh copy of my fork and follow the README step-by-step to see what a newcomer finds in their environment setup. I'll report back what I find.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5900274210

I reproduced the mismatch on a fresh clone of my fork on Windows 10 with Git Bash, comparing what the documentation asks for against what `.env.example` provides.

**Environment**

- OS: Windows 10 (build 19045.6466), shell: Git Bash (MINGW64)
- git 2.43.0.windows.1
- Code state: fresh clone of my fork `kingjaiteh/pathreview-ai301-fa26-s1` at `f89c06fc3ff292df2a04a39ac51319d32a76b779` (2026-09-16), the same commit as `codepath/pathreview-ai301-fa26-s1` `main`

```
$ git log -1 --format='%H %ad' --date=short
f89c06fc3ff292df2a04a39ac51319d32a76b779 2026-09-16
$ git --version
git version 2.43.0.windows.1
$ cmd //c ver

Microsoft Windows [Version 10.0.19045.6466]
```

**Steps**

Following the README's Quick Start in Git Bash, which the README recommends for Windows:

1. `git clone https://github.com/kingjaiteh/pathreview-ai301-fa26-s1.git` then `cd pathreview-ai301-fa26-s1`
2. `cp .env.example .env` (the Quick Start's configure step)
3. Compare what the docs tell you to set against what the new `.env` contains, using the commands below.

I stopped after the `.env` step without running `docker compose up -d` or `make setup`, because those steps can't change what the docs say or what the template contains.

**Output**

```
$ grep -n "OPENROUTER_API_KEY" README.md docs/SETUP.md
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
$ grep -c "OPENROUTER_API_KEY" .env
0
$ grep -n -A3 "# LLM provider" .env
16:# LLM provider
17-# Options: "mock" (default, no API key needed), "openai"
18-LLM_PROVIDER=mock
19-OPENAI_API_KEY=sk-your-key-here
$ grep -n "api_key\|llm_provider" core/config.py
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
```

**What this shows**

Both `README.md` and `docs/SETUP.md` tell users to set `OPENROUTER_API_KEY`, but `grep -c` shows it appears zero times in the generated `.env` file. The LLM provider comment in `.env` lists only "mock" and "openai" as options, without mentioning openrouter. `core/config.py` defines the field `openrouter_api_key`.

## Eval iterations

# Reproduction

## Run history

First run (smoke test, --limit 1): 1/1 agreement. Single package test to verify the rubric structure was working.

Second run (full evaluation): 17/20 agreement, below the 18/20 passing bar. Failed on pkg-03, pkg-09, and pkg-10, all gold accept. All three failures were on `claims-backed` alone—honest reports, two of them cannot-reproduces, that described their own procedure in prose.

Third run (canaries with --only): 6/6 agreement on pkg-03, pkg-09, pkg-10, pkg-20, pkg-02, and pkg-08. After revising `claims-backed` to allow first-person procedure accounts, all three previous misses flipped to accept, and the wrong-target and disclosure rejections held.

Fourth run (final full evaluation): 20/20 agreement, achieving the 18/20 pass bar. The revision to `claims-backed` resolved all discrepancies without introducing new failures.

## Package analysis

pkg-09 (sharkdp/fd#2033) first flipped to accept in the `--only` canary run and held in the confirming full evaluation. My rubric returned `accept`; gold labels accept it. The gold note is: "honest cannot-reproduce: real attempt at the argument-size reordering with marker-order artifacts, names what differed (uniform name lengths, 2 MiB ARG_MAX) and what a triggering setup likely needs." The initial rejection was a false negative: the author described their own procedure in prose ("I ran this setup and tried these variations"), and the first version of `claims-backed` demanded a separate pasted artifact for every claim about what they did. The revised check passes this because it separates claims into kinds—procedure claims on their own do not need separate artifacts as long as one pasted artifact shows the main result, which the marker-order output does.

## Check rationale

`claims-backed`: "No claim reaches past its evidence. A claim to have reproduced or confirmed the issue is backed only when a pasted artifact shows the issue's own behavior. Claims that generalize beyond the author's own runs ("every machine", "everyone", "all versions") or state a root cause as fact fail unless a pasted artifact shows them. The author's first-person account of their own procedure (how many times they ran it, variations and control runs they tried, what they changed between attempts) does not need a separate artifact per sentence, provided at least one pasted artifact shows the main result. A root-cause idea explicitly labeled as a guess or hypothesis passes. A cannot-reproduce stated with its evidence passes."

The first version treated prose about experimental procedure the same way it treated root-cause claims—both required separate pasted artifacts. This punished thoroughness. Pkg-09, pkg-03, and pkg-10 all failed because they described in words what they did, not because the artifacts were missing. The revision distinguishes what needs proof (did you see the issue?) from what's inherently honest (did you try five times or three?). The check now trusts the author's account of their own procedure as long as the main result is shown, which lets honest, detailed reports through without requiring a screenshot per experiment.

## Trade-offs

The loosened `claims-backed` enables strong procedure claims without pasted artifacts for every variation—a necessary cost to pass honest reports. The trade-off is that a report could now claim "I ran it five times" without having actually done so and still pass the check, because only the main result has to be pasted. The three canary re-runs with `--only` (pkg-03, pkg-09, pkg-10) all flipped to accept without opening new failure paths: wrong-target rejections (pkg-02, pkg-08) and the disclosure failure (pkg-20) remained rejected, showing the revision does not accidentally enable other kinds of bad packages.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
