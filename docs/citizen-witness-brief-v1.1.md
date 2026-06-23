# Citizen Witness — Post-Hoc Brief v1.1

**Concept:** A post-encounter evidence brief generator. Feed it a recording. It produces a structured, lawyer-ready document analyzing the interaction for constitutional violations and procedural failures.

**v1.1 Change:** Five pattern-detection hooks embedded into template sections — timing gap, charge mismatch, officer statements, spoliation/device handling, ambiguity scale. These are prompts the brief generator must answer, not optional.

**Status:** Scoped, not built.
**Parent:** Watching the Watchmen rail (NotebookLM notebook)

---

## v1.1 Scope: First Amendment Retaliation + Pattern Detection

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
    → Pattern Match (Bailey, Novak, Gonzalez + five recurrence patterns)
      → Brief Output
```

---

## Brief Output Sections (7 sections + detection hooks)

### 1. Timeline
Second-by-second log of the encounter: who spoke, what was said, what action was taken.

**Detection hook — Timing Gap:**
- What is the exact lag between the protected speech and the arrest/encounter?
- [ ] Hours or less — could be argued as split-second
- [ ] Days — undermines split-second justification under *Nieves*
- [ ] Weeks — strongly suggests deliberation and retaliatory planning
- Did the officer have time to investigate before acting? If yes, flag it. This contradicts the "split-second decision" qualified immunity defense.

### 2. Speech Analysis
Was the speech protected? What type? Where does it fall on the ambiguity scale?

**Detection hook — Ambiguity Assessment:**
- [ ] **Zero ambiguity** — petition, political criticism, public meeting speech (Gonzalez tier)
- [ ] **Some ambiguity** — parody, satire that some people misunderstood (Novak tier)
- [ ] **High ambiguity** — could be interpreted as a threat (Bailey tier)
- The less ambiguous, the stronger the First Amendment claim. The scale predicts remedy: damages (Bailey) → blocked by QI (Novak) → doctrine change (Gonzalez).

### 3. Probable Cause Check
Did the officer state a lawful reason for the stop/arrest/detention?

**Detection hook — Charge Mismatch / Collapsing Charges:**
- What was the initial charge?
- [ ] Charge was obviously pretextual (terrorism for a joke)
- [ ] Charge was arguable but unusual (felony for parody disruption)
- [ ] Charge was technically valid but never used this way before (tampering for a petition)
- Did charges get dropped, reduced, or result in acquittal? If yes, flag it.
- Was the enforcement disproportionate to the alleged offense? (SWAT for a Facebook post? Special detective for a document mix-up?)
- **Nieves check:** Was there probable cause? If yes, does the Nieves exception apply? (Statistical evidence the charge is never used this way, no comparator needed per *Gonzalez*.)

### 4. Rights Violations
Checklist: Miranda, search consent, excessive force, retaliatory motive.

**Detection hook — Officer Statements:**
- Did any officer make on-record comments about the speech itself?
- [ ] Statements expressing annoyance at the speech
- [ ] References to "making an example"
- [ ] Comments about the citizen's politics, posts, or opinions
- [ ] Language in the warrant affidavit suggesting retaliatory motive
- Collect verbatim quotes. Officer statements about the speech go directly to causation.

### 5. Pattern Match
Comparison to known IJ cases and the five recurrence patterns.

**Detection hook — Recurrence Checklist:**
- [ ] **Disproportionate escalation** — was the response unusual for the alleged offense?
- [ ] **Collapsing charges** — were charges dropped, dismissed, or resulting in acquittal?
- [ ] **Timing gap** — was there a deliberative delay between speech and enforcement?
- [ ] **Officer statements** — did any official comment on the speech itself?
- [ ] **Spoliation** — were devices seized or recordings missing?

For each flagged pattern, cite the relevant case (Bailey, Novak, Gonzalez) and describe how this encounter matches or differs.

### 6. Spoliation Flag
If the recording ends or is interrupted while in officer custody, note the gap and its legal significance.

**Detection hook — Device Handling:**
- [ ] Was the citizen's device (phone, recorder, camera) seized by police?
- [ ] Was body cam or dash cam footage available? If not, why?
- [ ] Was any recording interrupted, deleted, or "lost" while in police custody?
- [ ] If using a tamper-proof recorder: was it silenced or disabled? Timestamp the gap.
- **Legal significance:** Missing footage under state control = spoliation inference. The absence of expected evidence becomes evidence. Cite *Guardian Ad Litem* device concept: if the device is designed to be tamper-proof and goes silent in custody, the gap itself supports an adverse inference.

### 7. Next Steps
Preserve evidence, contact IJ or local civil rights attorney, file complaint.

**Detection hook — Absence Track:**
- What evidence *should* exist here but doesn't?
- [ ] No recording at all — why?
- [ ] No body cam / dash cam — was it "malfunctioning"?
- [ ] No independent witnesses — were any excluded or intimidated?
- [ ] No written report matching the citizen's account — discrepancy?
- Flagging what's missing is as important as documenting what's present. An absence track prevents the system from only seeing retaliation and missing genuine non-retaliatory encounters.

---

## Architecture

Same rails as everything else. Different domain, identical pattern:
```
Video recording → Whisper (transcribe) → NotebookLM (analyze against IJ case law)
  → Structured brief with detection hooks → Human review → Lawyer handoff
```

**What already exists:**
- NotebookLM ingestion pipeline (sources, prompts, synthesis)
- IJ case card — Bailey, Novak, Gonzalez facts + pattern library
- Governance pattern: fail-open, human gate before action
- Pattern discovery notebook (Citizen Witness — Pattern Discovery, 8 sources)
- Five recurrence patterns confirmed by cross-case NotebookLM synthesis

**What needs building:**
- Transcription layer (Whisper or equivalent)
- Brief output template with detection hooks wired
- Absence track (negative-space questions to balance pattern detection)

---

## Acceptance Criteria (v1.1)

- [ ] Accepts one recording (video or audio)
- [ ] Produces a structured timeline with speaker labels
- [ ] Answers all five detection hooks: timing gap, charge mismatch, officer statements, spoliation, ambiguity scale
- [ ] Cross-references Bailey, Novak, and Gonzalez as comparison patterns
- [ ] Flags the five recurrence patterns when present
- [ ] Runs the absence track (what evidence should exist but doesn't)
- [ ] Outputs a single markdown brief with all 7 sections
- [ ] Runs entirely on local infrastructure (no cloud dependency)
- [ ] Brief is human-reviewed before any external use

---

## Why Post-Hoc First

Spoliation doctrine works at the post-hoc layer: the absence of a recording becomes evidence when there IS a system designed to preserve it. A structured brief that a lawyer can file — and that a system like IJ can pattern-match across thousands of encounters — builds the database that changes law.
