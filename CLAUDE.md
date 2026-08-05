
## Cognitive system: Brain (linked via `brain` CLI)
This project is linked to the Brain cognitive system. Do not read the node
repos directly — use the CLI.

**How to invoke it (try in order, use the first that runs):**
1. `brain <cmd>`
2. if `brain` is not found: `python "$HOME/.brain/Brain/bin/brain" <cmd>`
   (Windows PowerShell: `python "$env:USERPROFILE\.brain\Brain\bin\brain" <cmd>`)

When the user asks anything like "query save" / "ask brain X" / "mine this",
run the matching `brain` command yourself — do not make the user type paths.
Before non-trivial work: `brain query <terms>`. To capture lessons, write a
proposal file + `brain sync` (or `brain mine` for a work-list). `brain sync`
reconciles with main. Keep session output minimal.

### Using Brain well (read this before deciding it's empty)
- **Query with 1-2 KEYWORDS, not sentences.** `brain query reachability`, not
  `brain query "ai cannot reach the exit on a walled map"`. The matcher is
  keyword-based; long phrases return 0. **A 0-result query almost always means
  rephrase, not "empty system"** — try broader / single terms first, and read
  the `local:` bucket, not just the shared counts.
- **Re-query at each NEW sub-problem, not only at session start.** Every
  non-trivial bug or decision is its own retrieval trigger.
- **Capture non-bugs too, not only bugs:** reusable pattern -> `ideas`;
  unresolved fork -> `tension`; experiment/synthesis -> `exploration`; a
  committed decision -> an ADR in the build (and if it generalizes, ALSO an
  `ideas` kernel). See `orchestration.md`'s write-back table.
- **At each milestone, produce a Cognitive Update UNPROMPTED** (New Ideas,
  Memory, Tensions, Exploration, Graduation Candidates) — the standing rule in
  `orchestration.md`.
- **Surface any open (red/yellow) tension that touches your work to the user**
  before committing to that fork.
- Schema: memory proposals use `## FULL ENTRY` + `## PROPOSED INDEX LINE`;
  tensions/exploration use `### ` blocks. Malformed entries are held on `sync`.

## Working format (agreed 2026-08-03, after a session that broke all five)

Each rule below is here because it was violated, with the cost noted. Check
these, don't just read them.

1. **Run `brain stance` at session start and obey it.** It was set to `brief`
   for an entire session while replies ran to multi-paragraph essays with
   headers. The stance is a standing instruction, not a preference — `brain
   stance --verbose` prints the card.
2. **`brief-gate` is on: challenge a vague brief BEFORE planning.** A vague
   brief got five rounds of confidently wrong work before anyone asked what it
   meant. Ambiguous ask → one clarifying question first, not a guess plus a
   correction cycle.
3. **Query Brain by GENRE, not just by sub-problem.** Querying `camera`,
   `reachability` and `analyze density` never surfaced `test.md#E10`
   ("a chronicle is not a story"), which described the exact artifact and
   exact failure a month earlier. Cost: four polish passes that each verified
   green and fixed nothing. Trigger: before the SECOND fix on one artifact,
   and whenever a complaint moves to a new surface, query the artifact's genre
   ("story", "pacing", "audio", "score").
4. **A claim of verification requires the artifact.** Two false claims in one
   session: a source comment asserting "want/opposition/stakes/choice,
   but/therefore, not a chronicle" over lines where 14 of 21 transitions were
   "and then"; and a reported watch-through whose monitoring loop
   (`until ! pgrep -f <name>`) matched its own command line, waited on itself
   forever, and never ran the sweep. Rule: paste the number, the log line or
   the measurement, or say "not verified" — and never let a comment stand in
   for a test that was never executed.
5. **Cognitive Update at each milestone, unprompted** — it is a standing rule
   above and was skipped for most of a long session. Non-bugs count: reusable
   pattern → `ideas`, unresolved fork → `tension`.

Standing consequence of (4): when something is genuinely unverified, say so in
the same breath as shipping it. Shipping with a named gap is fine; shipping
with an implied all-clear is not.
