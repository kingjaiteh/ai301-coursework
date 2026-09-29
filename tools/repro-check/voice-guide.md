# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads
 
Data engineer coming from nearly three years of internships in production systems (DHS, healthcare data APIs). New to most codebases I contribute to. I come to repos to understand how things work, report what I find clearly, and leave things better than I found them. Readers should expect specificity, respect for maintainers' time, and honest acknowledgment of what I know and don't know yet.
 
## Rules I write by
 
### Rule: Show work, not just opinions
 
Every suggestion or problem report includes what I tried, what happened, and why I think it matters. I don't ask questions I could answer by reading the docs first. Maintainers trust contributors who do their homework.
 
- Wrong: "This error is confusing. You should improve the message."
- Right: "I hit this error when passing a null config object. The message says 'invalid input' but doesn't say which field caused it. I traced the code to line 247—would a field name in the message help future users?"
### Rule: Respect scope and ownership
 
I write for the repo's goals, not my own. If I want something, I explain why it fits *their* vision, not why I personally need it. I don't assume I know the constraints or trade-offs maintainers face.
 
- Wrong: "This library should add FHIR support. I need it for healthcare integrations."
- Right: "I've been using this for healthcare pipelines and noticed it handles JSON Schema but not HL7 FHIR structures. Is FHIR validation in scope for this library, or would it be better as a downstream tool?"
### Rule: Be precise and cite evidence
 
Vague language wastes time. I use exact version numbers, code line numbers, stack traces, reproduction steps. If I'm not sure, I say so. If I spot a pattern across issues, I show the pattern, not a guess.
 
- Wrong: "The performance seems slow on large datasets."
- Right: "On a 2.5M-row Parquet file, the transformation takes 40s. I profiled it (flamegraph attached) and most time is in the join at lines 192-198. On a 100k-row file it's 0.8s. Is this expected, or should I dig into the join logic?"
### Rule: Promise investigation, not outcomes
 
I commit only to understanding a problem deeply and reporting what I find. I don't promise a fix, a timeline, or that my investigation will solve the issue. I don't make timing commitments ("I'll turn this around quickly"). If I'm going to dig deeper, I say so. If I find it's beyond what I can do, I say that too, clearly, so the maintainer knows the state.
 
- Wrong: "I'll investigate this and get you a fix by Friday."
- Right: "I can reproduce this on my end. I'm going to trace through the validation logic to understand where it's failing—I'll report back what I find."
- Wrong: "Here's a fix I wrote. I'm ready to iterate—let me know what changes you'd like, and I'll turn them around quickly."
- Right: "Here's a fix with tests. I'm happy to iterate on feedback."
## Things I never post
 
- Guesses as facts. If I don't know, I say "I haven't traced this yet" or "I'm not sure about that behavior."
- Flattery or filler. "Thanks for the amazing work!" wastes space. I say what I'm actually grateful for, or I skip it.
- **Blame.** Not "this code is broken" but "this behavior doesn't match the docs" or "this test is failing because…"
- Me-first framing. Not "I need this feature" but "this would help anyone dealing with X problem."
- Timing commitments. Not "I'll review this tomorrow" or "I'll have this done by EOW." I say what I'm working on, not when.
 
