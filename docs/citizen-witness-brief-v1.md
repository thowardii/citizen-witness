# Citizen Witness — Post-Hoc Brief v1

**Concept:** A post-encounter evidence brief generator. Feed it a recording. It produces a structured, lawyer-ready document analyzing the interaction for constitutional violations and procedural failures.

**Status:** Scoped, not built.
**Parent:** Watching the Watchmen rail (NotebookLM notebook)
**Sibling:** IJ Gift Scope (`ij-gift-scope.md`)

---

## v1 Scope: First Amendment Retaliation Only

Narrow for now. One pattern, done well:

**Trigger:** Any encounter where speech (verbal, written, online, symbolic) preceded a police response — arrest, citation, detention, or threat thereof.

**Inputs:**
- Video/audio recording of the encounter
- Officer name/badge (if known)
- Jurisdiction (city, county, state)
- Date/time/location
- Any prior speech that triggered the encounter (social media post, protest sign, verbal statement)

**Pipeline:**

```
Recording → Transcript → Structured Timeline
  → Rights Checklist (Miranda, probable cause, search justification)
    → Pattern Match (Bailey, Novak, other IJ retaliation cases)
      → Brief Output
```

**Brief Output Sections:**

1. **Timeline** — second-by-second log of the encounter: who spoke, what was said, what action was taken
2. **Speech Analysis** — was the speech protected? (satire, political opinion, criticism of government, petitioning)
3. **Probable Cause Check** — did the officer state a lawful reason for the stop/arrest/detention?
4. **Rights Violations** — checklist: Miranda, search consent, excessive force, retaliatory motive
5. **Pattern Match** — comparison to known IJ cases (Bailey: Facebook joke → SWAT → terrorism charge; Novak: critical Facebook posts → retaliatory arrest)
6. **Spoliation Flag** — if recording ends or is interrupted while in officer custody, note the gap and its legal significance
7. **Next Steps** — preserve evidence, contact IJ or local civil rights attorney, file complaint

---

## Architecture

Same rails as everything else. Different domain, identical pattern:

```
Video recording → Whisper (transcribe) → NotebookLM (analyze against IJ case law)
  → Structured brief → Human review → Lawyer handoff
```

**What already exists:**
- NotebookLM ingestion pipeline (sources, prompts, synthesis)
- IJ case card (`ij-retaliation-card.md`) — Bailey facts, legal spine, category-error analysis
- Governance pattern: fail-open, human gate before action
- Weekly brief pipeline (Pepperoni BI pattern, domain-mapped)

**What needs building:**
- Transcription layer (Whisper or equivalent)
- First Amendment retaliation prompt template (what to extract, what to flag)
- Bailey-pattern cross-reference (satire → threat classification → SWAT → terrorism charge)
- Brief output template (markdown, lawyer-ready)

---

## Acceptance Criteria (v1)

- [ ] Accepts one recording (video or audio)
- [ ] Produces a structured timeline with speaker labels
- [ ] Flags: Miranda, probable cause, search consent, retaliatory motive
- [ ] Cross-references Bailey case as comparison pattern
- [ ] Outputs a single markdown brief with all 7 sections
- [ ] Runs entirely on local infrastructure (no cloud dependency)
- [ ] Brief is human-reviewed before any external use

---

## Why Post-Hoc First

The real-time coaching layer is emotionally powerful but legally secondary. A judge doesn't care what the app whispered. They care about the record. The brief is the artifact that changes outcomes.

Spoliation doctrine works at the post-hoc layer: the absence of a recording becomes evidence when there IS a system designed to preserve it. Real-time coaching doesn't deter misconduct retroactively. A structured brief that a lawyer can file — and that a system like IJ can pattern-match across thousands of encounters — builds the database that changes law.

---

## Connection to IJ Gift

The IJ gift scope (`ij-gift-scope.md`) is intake-to-resolution case flow. The Citizen Witness brief is evidence generation. Two different lanes:

| | IJ Gift | Citizen Witness |
|---|---|---|
| What it does | Intake form → case pipeline → SLA → weekly brief | Recording → transcript → rights analysis → brief |
| Who it serves | IJ intake team | Citizen who just had an encounter |
| Output | Tracked case, response within 48h | Lawyer-ready brief |
| When built | After Pepperoni proves the pattern | After NotebookLM/Whisper pipeline is wired |

Both use the same architecture. Both run on the same platform. Both embody the same principle: the system doesn't punish — it triages, annotates, and escalates to human review.
