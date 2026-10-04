# Fix plan for #73

## Repro evidence this plan relies on

From my reproduction on #73 (https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5900274210), fresh clone of my fork at `f89c06fc3ff292df2a04a39ac51319d32a76b779`, Windows 10, Git Bash:

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

## Diagnosis

The evidence points one direction: `README.md:24` and `docs/SETUP.md:47` both instruct users to set `OPENROUTER_API_KEY`, and `core/config.py` lines 18–20 define `llm_provider`, `openai_api_key`, and `openrouter_api_key`. The template file `.env.example` is the outlier: it omits `OPENROUTER_API_KEY` entirely, while its `LLM_PROVIDER` comment lists only `mock` and `openai` as options.

## Scope

In scope:

- Adding `OPENROUTER_API_KEY` to `.env.example`

Not in scope:

- Wiring the LLM provider selection into code
- Other environment variables in `.env.example` (database ports, etc.)
- Changing `README.md` or `docs/SETUP.md` (they already agree with each other)
- Removing `OPENAI_API_KEY` (the embeddings provider reads it from the environment)

## Files

- `.env.example`

## Approach

After line 19 (`OPENAI_API_KEY=sk-your-key-here`), add a new line:

```
OPENROUTER_API_KEY=sk-or-your-key-here
```

This places the OpenRouter key in the same section as the OpenAI key, under the LLM provider comment, so the template lists every key the docs and `core/config.py` name.

## Test plan

Re-run the same commands from my repro on this branch, from a fresh copy of the template:

```bash
rm -f .env && cp .env.example .env
grep -c "OPENROUTER_API_KEY" .env
grep -n -A4 "# LLM provider" .env
```

Before the fix (my posted repro):

- `grep -c "OPENROUTER_API_KEY" .env` printed `0`
- The LLM provider block showed `LLM_PROVIDER=mock` and `OPENAI_API_KEY`, with no OpenRouter key

After the fix:

- `grep -c "OPENROUTER_API_KEY" .env` should print `1`
- The LLM provider block should show lines 16–20: the comment, `LLM_PROVIDER=mock`, `OPENAI_API_KEY=sk-your-key-here`, and `OPENROUTER_API_KEY=sk-or-your-key-here`

## Risks and unknowns

Nothing in the codebase outside `core/config.py` reads `llm_provider`, `openai_api_key`, or `openrouter_api_key` at this commit, so this change updates the template without affecting runtime behavior. I'm deliberately not adding "openrouter" as an option in the `LLM_PROVIDER` comment, because nothing reads `LLM_PROVIDER`, so I can't verify that value does anything. PR #77 (by a classmate) also edits `README.md` and `.env.example`, so there's a merge-conflict risk if it lands first. The CI pipeline has five jobs that must pass even on a docs-only change.

## Deviations

nothing changed from the plan.