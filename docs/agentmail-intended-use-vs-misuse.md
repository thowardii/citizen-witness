# AgentMail — Intended Use vs. Documented Misuse

**Research date:** June 22, 2026
**Sources:** AgentMail Terms of Service (May 11, 2026), HN Show HN thread (108 comments), YC launch page

---

## Intended Use (Per AgentMail)

- API-first email infrastructure for AI agents
- Transactional and programmatic email use ONLY
- Two-way communication between agents and humans
- Agents processing email so humans don't have to read spam/slop
- "The internet was made for humans — we're making it work for agents"

**Product:** Email API + LinkedIn API + Cadences (sequences)

---

## Stated Prohibitions (Acceptable Use Policy §4)

Their words:
- "MyAgentMail is transactional email infrastructure, **not a marketing relay**"
- Violations = "immediate suspension without prior notice"
- "The first communication you receive from us in response to a suspected violation may be the suspension itself"

**Prohibited:**
- Phishing, malware, deception
- Brand impersonation (PayPal, DHL, banks, government agencies)
- Unsolicited bulk email (marketing, newsletters, cold-list outreach)
- Non-opted-in recipients (purchased, scraped, harvested, guessed)
- Mass identical-content sends (spam/phishing pattern)
- Programmatic mass provisioning (dozens of inboxes in minutes to evade limits)
- Anything illegal under POPIA, GDPR, CAN-SPAM, CASL, PDPA
- Circumvention of safeguards

---

## Documented Misuse (HN Community, May 2026)

### 1. Unsolicited AI-Generated Outreach
- HN user received email from `kushal@kushalsm.com` — an agentmail.to address — pitching Chrome Relay to someone who asked about WebSocket auth on a completely different forum
- The email appeared personal ("Saw your question on the Agent Vault thread...") but was sent by an AI agent scraping forums
- Recipient's email was never used for signup — it was harvested or guessed
- **The agent email pitch is the abuse pattern:** AI scrapes public conversations → generates "personalized" outreach → sends via AgentMail

### 2. Misrepresentation of AI Origin
- Paid users CAN send from custom domains, hiding the agentmail.to origin
- Free tier users forced to use agentmail.to addresses — the founder called this a feature so "you can have an easier time identifying LLM emails"
- HN response: "And for paid users the receivers don't need to have an easier time identifying the LLM email? What kind of reasoning is that?"
- Proposed "sent via AgentMail" footer is meaningless to most recipients — they won't know what AgentMail is

### 3. Legal Violations Already Occurring
- Germany's §7 UWG makes unsolicited marketing emails illegal
- UK ICO direct marketing regulations violated
- CAN-SPAM and CASL compliance questionable for agent-initiated outreach
- One HN user: "I hate this so much and this is going to be a nightmare"

### 4. Pattern-Matched as Spam Service
- HN user: "Just go post on black hat forums. Plenty of people want this, it's a spam service. You don't need to be here."
- Multiple users identified the architecture itself enables spam at scale
- AI agents + email API + custom domains = untraceable automated outreach

### 5. LinkedIn + Email = Full-Stack Impersonation
- AgentMail also offers LinkedIn API and "Cadences" (automated sequences)
- An AI agent can now: scrape your profile → find your email → send personalized cold outreach → follow up on LinkedIn
- All from one API key

---

## The Architecture Problem

Same pattern as Flock but different domain:

| | Flock | AgentMail |
|---|---|---|
| Claimed use | Crime-solving tool | Transactional email for agents |
| Architecture | Nationwide camera network + search | Email API + custom domains + LinkedIn |
| Abuse vector | Warrantless surveillance, profiling | AI-generated spam, impersonation, unsolicited outreach |
| Who's harmed | Protesters, minorities, women | Anyone with a public email or forum presence |
| Safeguard failure | Audit logs exist but don't prevent abuse | AUP exists but enforcement is reactive (after suspension) |
| Scale of abuse | 4M warrantless searches/year, 83K cameras | Unknown — but every agentmail.to user can reach thousands |

**The architecture IS the abuse vector.** The safeguards (AUP, audit logs, rate limits) are after-the-fact. The infrastructure itself enables harm at scale before any human reviews it.

---

## What This Means

AgentMail is the email equivalent of what Flock is to surveillance: infrastructure that enables behavior its own terms prohibit. The business model requires scale. Scale creates abuse. The abuse is documented. The safeguards are reactive.

When Tom says "find out what their intended uses are and what they consider misuse" — the answer is: **the intended use is transactional email for agents. The misuse is everything the AUP prohibits. And the misuse is already happening at scale, documented in public 31 days after launch.**
