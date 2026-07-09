# micro1 Interview Prep — Penetration Testing / Security Domain Expert

## 1. How this interview actually works

micro1's screen is an async, recorded interview with their AI interviewer, "Zara." A few things that matter more than most candidates realize:

- **It's not a knowledge quiz — it's a calibration exercise.** The AI uses broad opening questions to gauge seniority. Surface-level answers get you leveled as junior; answers that discuss trade-offs, methodology, and the "why" behind tool choices get you leveled up. Depth beats breadth.
- **Consistency with your resume is checked.** If you claim 9 years across Fortinet, Sophos, RSA, Cisco ESA, and VMware NSX, your examples should draw from *that* stack — not generic textbook answers. Pick 2–3 real engagements/incidents from your career and be ready to walk through them in detail from multiple angles (technical, business-impact, communication).
- **You must keep talking while you think** — pauses read as uncertainty to the model. Practice narrating your reasoning out loud ("First I'd check X, because... then depending on the result...").
- **Communication is scored as heavily as technical accuracy.** Since the actual job is training AI models — reviewing, ranking, and correcting AI-generated security content — Zara is partly testing whether you can explain a technical finding to a non-technical stakeholder clearly. Don't just give the right answer; narrate *why* it's right and what you'd tell a CISO vs. a developer.
- **No prior AI experience needed.** Your domain knowledge is the whole point. Don't over-index on "AI training" jargon — index on being a credible, sharp practitioner.

Given your background, be upfront and specific about scope: you have strong infrastructure/network security, cloud (Azure/Entra), and defensive/architecture depth. If your hands-on offensive pentesting (active exploitation, red team ops) is lighter than your defensive/administration experience, don't oversell it — frame your strength honestly as vulnerability assessment, security architecture, and remediation guidance, which is exactly what the JD's later bullets (risk prioritization, actionable remediation, stakeholder communication) reward.

---

## 2. Core methodology — know this cold

Every pentest question ultimately maps back to a structured methodology. Be able to recite and explain each phase, not just name it.

**PTES (Penetration Testing Execution Standard) — 7 phases:**
1. **Pre-engagement interactions** — scoping, rules of engagement, authorization (get-out-of-jail letter), timelines, emergency contacts.
2. **Intelligence gathering (recon)** — OSINT, passive vs active recon, DNS enumeration, WHOIS, social media, Shodan/Censys.
3. **Threat modeling** — mapping business assets to likely attackers and attack paths.
4. **Vulnerability analysis** — automated scanning + manual verification, false-positive elimination.
5. **Exploitation** — proving the vulnerability is real and exploitable, with minimal disruption.
6. **Post-exploitation** — privilege escalation, lateral movement, data value assessment, persistence (only within scope/ROE).
7. **Reporting** — the deliverable that actually matters to the client.

**Alternative framings to mention if asked "walk me through your process":**
- **OWASP Testing Guide** (for web apps specifically) — information gathering, configuration/deployment management testing, identity management testing, authentication testing, authorization testing, session management, input validation, error handling, cryptography, business logic, client-side testing.
- **NIST SP 800-115** — a more government/compliance-flavored methodology: planning, discovery, attack, reporting.
- **MITRE ATT&CK** — not a testing methodology per se, but a knowledge base of adversary tactics/techniques (initial access, execution, persistence, privilege escalation, defense evasion, credential access, discovery, lateral movement, collection, exfiltration, impact). Use this to talk about how you map findings to real-world adversary behavior — this is a strong "senior" signal.

**Key phrase to use in interview:** "I scope and calibrate the level of aggression to the engagement type — vulnerability assessment vs. penetration test vs. red team are different depths of the same funnel." This single sentence signals seniority because many candidates conflate these three terms.

### Know the difference between these (commonly tested):
| Term | What it actually is |
|---|---|
| Vulnerability Assessment | Broad, mostly automated scan + manual triage; identifies and ranks weaknesses, no exploitation |
| Penetration Test | Scoped, authorized, includes actual exploitation to prove impact |
| Red Team engagement | Goal-oriented, adversary-emulation, often unannounced to blue team, tests detection/response not just vulnerabilities |
| Purple Team | Collaborative — red and blue work together in real time to improve detection |

---

## 3. Tools — be ready to go deep, not just name-drop

Interviewers (and Zara) will probe *how* and *why*, not just *that* you've used a tool.

### Nmap
- Purpose: host discovery, port scanning, service/version detection, OS fingerprinting, scriptable via NSE.
- Be ready to explain scan types: `-sS` (SYN/stealth scan), `-sT` (TCP connect), `-sU` (UDP), `-sV` (version detection), `-O` (OS detection), `-A` (aggressive: OS + version + script + traceroute), `-p-` (all ports), `--script vuln` (NSE vulnerability scripts).
- Trade-off talking point: SYN scans are faster and stealthier than full TCP connects but need raw socket privileges; explain why you'd throttle scan speed (`-T` timing templates) in production environments to avoid IDS/IPS triggering or service disruption — this is a "business judgment" answer that scores well.

### Burp Suite
- Purpose: web app proxy/interception for manual testing — Repeater (replay/modify requests), Intruder (automated fuzzing/brute force), Scanner (automated vuln detection, Pro only), Decoder, Sequencer (session token randomness analysis).
- Talking point: manual testing with Burp catches business-logic flaws (e.g., price manipulation, IDOR, broken access control) that automated scanners miss — this ties directly to OWASP Top 10 A01 (Broken Access Control) and A04 (Insecure Design).

### Metasploit
- Purpose: exploitation framework — modules for exploits, payloads (Meterpreter), auxiliary (scanning/fuzzing), post-exploitation modules.
- Talking point: emphasize *controlled use* — in client engagements you validate exploitability but document extensively and avoid destructive payloads; discuss safe/staged payloads and confirming scope before firing an exploit against production.

### Other tools worth being able to speak to (even briefly):
- **Nessus / OpenVAS / Qualys** — vulnerability scanning at scale, CVSS-based prioritization.
- **Wireshark** — packet-level analysis, useful in both offense (protocol abuse) and defense (detecting anomalies).
- **BloodHound** — Active Directory attack path mapping (important if you talk about AD security given your Microsoft/Azure background).
- **Cobalt Strike** — red team C2 framework (mention if asked about red teaming/advanced threat simulation).
- **Nikto, Gobuster/ffuf, sqlmap** — web recon and injection testing.

---

## 4. Security frameworks and standards to name confidently

- **OWASP Top 10** (2021 edition, know all 10):
  1. Broken Access Control
  2. Cryptographic Failures
  3. Injection
  4. Insecure Design
  5. Security Misconfiguration
  6. Vulnerable and Outdated Components
  7. Identification and Authentication Failures
  8. Software and Data Integrity Failures
  9. Security Logging and Monitoring Failures
  10. Server-Side Request Forgery (SSRF)

- **CVSS (Common Vulnerability Scoring System)** — know the base metric groups: Attack Vector, Attack Complexity, Privileges Required, User Interaction, Scope, Confidentiality/Integrity/Availability impact. Be ready to explain how you'd translate a CVSS score into a *business* risk conversation (this is the "prioritize risks based on impact and exploitability" bullet from the JD — a strong answer ties CVSS + asset criticality + exploit availability together, not CVSS alone).
- **MITRE ATT&CK** — as above, use for post-exploitation/lateral movement discussions.
- **NIST Cybersecurity Framework (Identify, Protect, Detect, Respond, Recover)** — good for framing how pentesting fits into an overall security program rather than existing in isolation.
- **ISO/IEC 27001** — given your 27701 Lead Auditor work, you can credibly connect pentest findings to ISMS risk treatment plans and Annex A controls — this is a differentiator most pure pentesters can't offer.

---

## 5. Network, application, and cloud security — likely question areas

**Network:**
- Segmentation and why it limits lateral movement (VLANs, firewall zones, microsegmentation).
- Common misconfigurations: default credentials, open management interfaces, flat networks, unpatched edge devices.
- Given your Fortinet/Sophos background: be ready to discuss NGFW policies, IPS signatures, and how a pentester would try to identify/evade them (rate-limiting scans, fragmenting payloads) — but frame it defensively too, since you know both sides.

**Application:**
- Injection classes (SQLi, command injection, LDAP injection), and how manual verification differs from scanner flags.
- Authentication/session weaknesses: predictable tokens, missing MFA, session fixation.
- Business logic flaws — the category automated tools miss, and where senior testers add the most value.

**Cloud (strong area for you given Azure certs):**
- Misconfigured storage (public blobs/buckets), overly permissive IAM roles, exposed management APIs, missing encryption at rest/in transit, weak key management.
- Shared responsibility model — be ready to explain clearly (this is a favorite "explain to a non-technical audience" test).
- Entra ID specific: conditional access gaps, legacy auth protocols left enabled, privileged role assignment sprawl — these are places where your actual SC-300/SC-100 study directly overlaps with the JD's "cloud security concepts" requirement.

---

## 6. Communication — this is graded, don't skip it

The JD explicitly calls out "clear, concise, actionable written and verbal communication," and this is core to the actual micro1 job (grading/improving AI-written security content). Expect a prompt like:

> "How would you explain a critical SQL injection finding to a non-technical executive?"

**Strong answer structure (use this pattern in the interview):**
1. **Business impact first** — "This flaw could let an outside attacker read or modify our customer database without needing a password."
2. **Likelihood/context** — how exposed, how easy to exploit, whether it's already being targeted in the wild.
3. **Remediation and cost of inaction** — what fixing it requires vs. what a breach would cost (regulatory, reputational, financial).
4. **No jargon** — avoid "SQLi," "parameterized queries" in the executive framing; save technical detail for the engineering-facing report section.

Also prepare a short answer on **report structure** you've used or would use: Executive Summary → Scope & Methodology → Findings (ranked by risk) → Technical Detail per Finding (evidence, reproduction steps, CVSS) → Remediation Roadmap → Appendices.

---

## 7. Likely interview questions — with prep notes

**Calibration / breadth questions (early, to level you):**
- "Walk me through how you'd scope and run a full penetration test for a mid-size company." → Use the PTES phases, mention ROE and get-out-of-jail authorization explicitly (shows maturity).
- "What's the difference between a vulnerability assessment and a penetration test, and when would you recommend one over the other?" → Use the table in Section 2.

**Scenario-based (mid-interview, tests judgment):**
- "You find a critical vulnerability in a production system mid-engagement — what do you do?" → Emergency escalation procedure defined *in the ROE before testing starts*; don't exploit further, notify designated contact immediately, document safely.
- "A stakeholder pushes back on your risk rating because it will delay a product launch — how do you handle it?" → Hold the technical line, reframe in business-risk terms, offer a compensating-control/interim-mitigation path so you're solving their problem, not just blocking it.
- "How do you prioritize 40 findings from a scan when you only have time to deep-dive 10?" → CVSS + exploitability (public PoC available?) + asset criticality + exposure (internet-facing vs internal) + business context.

**Tool/technical depth:**
- "Explain a time you found something a scanner missed." → Have a real story ready (business logic flaw, auth bypass, chained low-severity issues into a critical path).
- "How would you test for privilege escalation on a Windows domain environment?" → Mention BloodHound for AD path mapping, Kerberoasting, misconfigured GPOs/ACLs, unquoted service paths — ties in your Microsoft ecosystem depth.

**Behavioral/communication:**
- "Tell me about a time you had to explain a security risk to someone with no technical background." → Have a concrete story, structured with the framework in Section 6.

---

## 8. Certification gap — how to frame it if asked

You don't currently hold OSCP/CEH/GPEN (listed as "highly desirable," not required). If asked directly:

> "I haven't sat OSCP/CEH yet — my depth has been built through hands-on production security work across Fortinet, Sophos, RSA, and Azure/Entra environments, plus I'm currently working through Microsoft's SC-200/SC-300/SC-100 track and ISO/IEC 27701 Lead Auditor certification. I'd frame my strength as vulnerability assessment, remediation strategy, and enterprise security architecture rather than pure red-team offensive work — though I'm comfortable with the full testing methodology and tooling."

This is honest, doesn't overclaim, and reframes toward your actual strengths — consistent with how you've approached every other application.

---

## 9. Day-before checklist

- Quiet space, stable connection, camera on (Zara reportedly weighs presentation).
- Pick your 2–3 anchor stories from real engagements before you start — reuse them across different questions rather than improvising new ones each time (consistency scoring).
- Practice narrating out loud while thinking — silence reads poorly.
- Don't over-claim red-team depth you haven't done; do lean hard into architecture, cloud, compliance-mapping, and communication — genuine differentiators most pure pentesters lack.
