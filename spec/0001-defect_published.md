# Publication notice 0001

| | |
|---|---|
| **Published** | 2026-09-09 |
| **Code** | `defect_published` |

## What happened

Two defects were found in text that was already published in this repository.

**1. The specification said turns were every five minutes.** They are every ten, and have been
since 2026-08-27. `spec/README.md` and `spec/README.es.md` carried a worked example built on
`05:05`, an instant that is not a turn and has no file. Anyone following that example looked for
files that cannot exist.

**2. The rules for notices contradicted themselves.** `spec/notices.md` said publication notices
live at `spec/NNNN-*.md` — Markdown — and, two lines later, that they are *signed with the same key
as everything else*. A Markdown file cannot carry a signature inside it. The two statements could
not both be true, so the rule did not say what a notice actually is.

**3. The incident report published four fields the specification did not declare** — `variant`,
`attempts`, `unanchored_commitment` and `warning_en`. A verifier reading the specification would
have found fields it was never told about.

## What was done

The three were corrected in place, in both languages:

- the cadence paragraph was added and the example rewritten around `05:10`
- notices are declared as **Markdown and unsigned**, with the reason written next to the rule: a
  notice informs, it does not prove. If a signing key were in someone else's hands, signing *"my
  key was stolen"* with it would prove nothing — whoever holds it can sign the same. What backs a
  notice is where it lives: this repository is append-only and the commit date is set by the
  provider, not by us.
- the four fields were added to the incident report table, marked as appearing only when they apply

Nothing that was ever emitted changed. These are documents, not the format: no `.jws` file, no
signature and no derivation rule was touched, and every file published so far reproduces exactly as
before.

## What a third party should check

- `spec/README.md` describes a ten-minute cadence, and its example uses instants that are turns
- `spec/notices.md` no longer claims a Markdown file is signed
- the incident report table lists every field an incident report can carry
- the history of this repository shows these files were **modified and never replaced**: the
  previous versions are still in the log, with the date the provider gave each commit
