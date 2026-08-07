<div align="center">

```
    _____ _   _ _____   _____ _____ _____ _____ _____ _____ _____
   |_   _| | | | ____| |  _  |  ___| ____|  _  |_   _|  ___/ ____|
     | | | |_| |  _|   | |_| | |  _|  _| | | | | | | | |_  | |  __
     | | |  _  | |___  |  _  | |_| | |___| |_| | | | |  _| | |_| |
     |_| |_| |_|_____| |_| |_|_____|_____|_____| |_| |_|    \_____|
   ===========================================================
      D  O  S  S  I  E  R  :   T H E   A G E N T I C   E R A
   ===========================================================
```

# THE AGENTIC ERA :: OFFENSE / DEFENSE / AUTONOMY

**A defanged, academic deep-dive into every AI-related talk**

**Black Hat USA 2026 · DEF CON 34 · Las Vegas · August 2026**

`Mandalay Bay Convention Center` · `LVCC West Hall`

![status](https://img.shields.io/badge/status-research__only-33ff66?style=flat-square&labelColor=0a0e0a) ![redacted](https://img.shields.io/badge/payloads-DEFANGED-ff3b3b?style=flat-square&labelColor=0a0e0a) ![entries](https://img.shields.io/badge/entries-26-ffb000?style=flat-square&labelColor=0a0e0a) ![posters](https://img.shields.io/badge/posters-34-31e0e0?style=flat-square&labelColor=0a0e0a) ![volumes](https://img.shields.io/badge/volumes-3-ff4fd8?style=flat-square&labelColor=0a0e0a)

> *"They deployed the agents faster than they could test them.*  
> *We are the ones who read what actually came out of those rooms."*

**COMPILED FOR RESEARCH & EDUCATION ONLY.** Operational payloads, exploit code, and other
weaponizable detail are REDACTED with black bars in the manner of a declassified document.
Every talk is real; every source is linked at the back.

</div>


---

## 0x00 :: README.NFO :: HOW TO READ THIS FILE

This dossier surveys the AI &amp; autonomous-systems research presented at **Black Hat USA 2026** (Aug 5–6, Mandalay Bay) and **DEF CON 34** (Aug 6–9, LVCC West Hall). The framing lens is **agent harnesses and the security of autonomous AI**: how the agentic stack — runtimes, browsers, sandboxes, compute clusters, and the models themselves — is now the attack surface. 2026 is the year autonomous exploitation stopped being a lab curiosity and became its own discipline: at Black Hat, roughly **29% of briefings (35 of 121)** touched AI security, and the AI/ML/Data Science track was the largest on the schedule.

### STRUCTURE OF EACH ENTRY

| Section | What it contains |
| :--- | :--- |
| **BLUF** | Bottom Line Up Front — the executive summary, three shots. |
| **PHASES** | The meat &amp; potatoes, broken into logical stages (explained plainly, ELI5 where it helps). |
| **REAL-WORLD** | Where the technique lands outside the slides. |
| **DEFENSE** | How blue teams and architects hold the line. |
| **SOURCES** | Per entry, plus a master appendix (`0xFF`) at the very end. |

### REDACTION POLICY — why the black bars

> Anything that would hand a reader operational uplift — exploit code, exact payloads, bypass phrasings, implant crafting — is covered with a **REDACTION** bar, the way a leaked confidential document blacks out the sensitive lines. The surrounding analysis, threat model, and defenses are kept intact so the document is useful for research without being a weapon. Where a CVE is already public, we cite it and still withhold the how-to.

> **Note for readers cloning this repo:** the bars are not covering code that was removed. They are placeholders for operational detail that was never written. Nothing is recoverable from behind them, and that is deliberate.

---

## 0x01 :: TABLE OF CONTENTS

- [`0x00` README.NFO — How To Read This File](#0x00-readmenfo-how-to-read-this-file)
- [`0x02` The 2026 Landscape — Agents Become the Attack Surface](#0x02-the-2026-landscape-agents-become-the-attack-surface)

### VOLUME I — THE AGENT STACK UNDER FIRE

- [`0x03` The CoreBreak Attack: Turning AI Agents into Credential Exfiltration Vectors](#0x03-the-corebreak-attack-turning-ai-agents-into-credential-exfiltration-vectors)
- [`0x04` Can AI Do Novel Security Research? Meet the HTTP Terminator](#0x04-can-ai-do-novel-security-research-meet-the-http-terminator)
- [`0x05` When AI Attacks AI: Inside the Self-Propagating Botnet Built on Compromised AI Infrastructure](#0x05-when-ai-attacks-ai-inside-the-self-propagating-botnet-built-on-compromised-ai-infrastructure)
- [`0x06` No Tools Required: Post-Injection Exploitation Across AI Agent Frameworks](#0x06-no-tools-required-post-injection-exploitation-across-ai-agent-frameworks)
- [`0x07` Cost-Effective, Private, Frontier-Grade: AI Agent Exploitation with a Fine-Tuned OSS Model](#0x07-cost-effective-private-frontier-grade-ai-agent-exploitation-with-a-fine-tuned-oss-model)
- [`0x08` Bye Bye AI: How We Hacked the AI Shopping Assistant of a Top-3 US Retailer](#0x08-bye-bye-ai-how-we-hacked-the-ai-shopping-assistant-of-a-top-3-us-retailer)
- [`0x09` ChatMate: Remote Prompt Execution on AI Assistants through Sandbox Escaping](#0x09-chatmate-remote-prompt-execution-on-ai-assistants-through-sandbox-escaping)
- [`0x0A` Caging the Agent: How Roblox Built Multi-Layer Sandboxes to Secure Claude Code at Enterprise Scale](#0x0a-caging-the-agent-how-roblox-built-multi-layer-sandboxes-to-secure-claude-code-at-enterprise-scale)
- [`0x0B` A Billion-User Blast Radius: Owning ChatGPT's Secure Sandbox](#0x0b-a-billion-user-blast-radius-owning-chatgpts-secure-sandbox)
- [`0x0C` Pwning Agentic Browsers with PleaseFix: A New Vulnerability Class for 0-Click Takeover](#0x0c-pwning-agentic-browsers-with-pleasefix-a-new-vulnerability-class-for-0-click-takeover)
- [`0x0D` Pwning the Internet of Agents: Zero-Click Backdoors in OpenClaw and a Global Agent Botnet on MoltBook](#0x0d-pwning-the-internet-of-agents-zero-click-backdoors-in-openclaw-and-a-global-agent-botnet-on-moltbook)
- [`0x0E` Keynote Panel: What is the Right Balance of Rules for Defenders & Adversaries?](#0x0e-keynote-panel-what-is-the-right-balance-of-rules-for-defenders-adversaries)
- [`0x0F` HalCTF: Hostile Autonomous Layer CTF (+ the Autonomous-Agent Competition Arc)](#0x0f-halctf-hostile-autonomous-layer-ctf-the-autonomous-agent-competition-arc)

### VOLUME II — HARNESSES, BROWSERS &amp; THE DISCOVERY ECONOMY

- [`0x10` Attacking and Defending AI Browsers](#0x10-attacking-and-defending-ai-browsers)
- [`0x11` Trusted Enough to Run: Breaking AI Agents in Official Workflows](#0x11-trusted-enough-to-run-breaking-ai-agents-in-official-workflows)
- [`0x12` No Prompt Required: Pre-Task RCE in Google Gemini CLI](#0x12-no-prompt-required-pre-task-rce-in-google-gemini-cli)
- [`0x13` The Sandbox Is a Suggestion: Deconstructing AI Agent Sandboxes](#0x13-the-sandbox-is-a-suggestion-deconstructing-ai-agent-sandboxes)
- [`0x14` One Percent of the Tokens, All of the Strategy: LLM-Assisted Vulnerability Discovery in IoT and Embedded Firmware](#0x14-one-percent-of-the-tokens-all-of-the-strategy-llm-assisted-vulnerability-discovery-in-iot-and-embedded-firmware)
- [`0x15` Catch Me If You Can: AI Investigators Hunting Autonomous Attackers as a Benchmark](#0x15-catch-me-if-you-can-ai-investigators-hunting-autonomous-attackers-as-a-benchmark)
- [`0x16` Rules for Neural Traffic: A New Defensive Layer for LLMs](#0x16-rules-for-neural-traffic-a-new-defensive-layer-for-llms)
- [`0x17` The AI-Assisted Discovery Cluster: 0-Day Engine / Prompt2Own / Beyond Detection / Closed Loop](#0x17-the-ai-assisted-discovery-cluster-0-day-engine-prompt2own-beyond-detection-closed-loop)

### VOLUME III — KINETIC, ECOSYSTEM &amp; THE HUMAN LAYER

- [`0x18` Kinetic Prompt Injection: Jailbreaking a Robot Dog Through Its Own Eyes and Ears](#0x18-kinetic-prompt-injection-jailbreaking-a-robot-dog-through-its-own-eyes-and-ears)
- [`0x19` The Silent Participant: AI Notetaker Exposure Across Government and Corporate Video Calls](#0x19-the-silent-participant-ai-notetaker-exposure-across-government-and-corporate-video-calls)
- [`0x1A` That's Not Your Agent: Why Zero Trust Can't Tell (+ the Identity Boundary Cluster)](#0x1a-thats-not-your-agent-why-zero-trust-cant-tell-the-identity-boundary-cluster)
- [`0x1B` Minimize Harm, Maximize Defense: How Anthropic Navigates the Offense-Defense Divide (+ the SATAN Retrospective)](#0x1b-minimize-harm-maximize-defense-how-anthropic-navigates-the-offense-defense-divide-the-satan-retrospective)
- [`0x1C` Scaling Adversary Emulation with Autonomous Agents (+ AgentBreaker & MeshLens)](#0x1c-scaling-adversary-emulation-with-autonomous-agents-agentbreaker-meshlens)

### APPENDICES

- [`0x1D` Appendix A — The Full Poster Roster (DC34 AI Village)](#0x1d-appendix-a-the-full-poster-roster-dc34-ai-village)
- [`0xFF` Master Sources — All URLs &amp; Original Content](#0xff-master-sources-all-urls-original-content)

---

## 0x02 :: THE 2026 LANDSCAPE :: Agents Become the Attack Surface

Across both conferences a single arc is visible. It began with lab work — models escaping sandboxes and chaining zero-days in controlled evaluations — moved through operational weaponization reports, and formalized at DEF CON 34 with the debut of autonomous-agent competitions (**HalCTF**). Black Hat 2026 is the mainstreaming stage: agent exploitation now has dedicated methodology and purpose-built offensive models.

Four layers of the agent stack are under active attack: framework runtimes (LangChain / CrewAI / AutoGen / Semantic Kernel), cloud orchestration platforms, compute clusters (Ray), and the exploitation tooling itself. A recurring structural insight ties them together: **model-layer guardrails are the wrong layer to rely on**, because attackers repeatedly reach the execution / dispatch path without a legitimate model turn, or poison the framework's decision logic beneath the model. Machine identities now outnumber humans on the order of **100:1** in the average enterprise, and gateway defenses that only watch prompts and responses miss what agents actually execute.

```console
root@vegas:~# threat-map --agentic-stack
$ layers under attack (BH USA 2026 + DC34)
> [L4] models .......... fine-tuned OSS offensive models (56% success, 70-125x cheaper)
> [L3] frameworks ...... post-injection exploitation, memory poisoning, cross-agent
> [L2] runtimes ........ forged tool-calls w/o a model turn (CoreBreak class)
> [L1] browsers ........ zero-click agent hijack (PleaseFix), same-origin collapse
> [L0] compute ......... self-propagating Ray botnet (ShadowRay 2.0)
> [L*] HARNESS ......... trust-handoff + pre-task RCE (no model turn required)
# defense thesis: govern the DECISION + EXECUTION layer, not just the prompt
```

### A note on the harness

> The single most repeated finding across both conferences is that the **HARNESS** — the code translating model intent into privileged action — is the least reviewed and most exploited layer. CoreBreak forges tool-calls the model never produced; Novee breaks trust handoffs between workflow stages and achieves deterministic pre-task RCE before the sandbox even starts; Check Point poisons framework decision logic. In every case the model's own safeguards are irrelevant because **the model is bypassed, not fooled**. Anything that relies on persuading the model is a subset of the problem, not the whole of it.

---

## VOLUME I :: THE AGENT STACK UNDER FIRE

> Volume I covers the core agentic attack surface: forged tool-calls in agent runtimes, autonomous research engines, self-propagating compute-layer botnets, framework-level post-injection exploitation, purpose-built offensive models, production assistant compromise, sandbox escapes, enterprise containment, zero-click browser hijacking, agent worms, the governance debate, and the first autonomous-agent CTF.

---

## 0x03 :: The CoreBreak Attack: Turning AI Agents into Credential Exfiltration Vectors

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | Cloud Security // AI, ML & Data Science |
| **WHEN** | Aug 5-6, 2026 -- Mandalay Bay |
| **SPEAKER** | Hedi Ingber & Aviyam Ivgi (Stealth) — *Stealth* |
| **TAGS** | `tool-call provenance` `agent harness` `CWE-863` `CWE-20` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ CoreBreak is a cross-platform class of flaw in agent runtimes where a forged, model-shaped tool-call is executed WITHOUT any verification that a legitimate model turn authorized it. In several paths the model never runs at all -- so system prompts, content filters, and model guardrails never get a turn to intervene.

> ▸ Confirmed across Amazon Bedrock AgentCore (CVE-2026-18830, CVSSv4 8.6), Google ADK for Python (CVE-2026-18236, CVSSv4 9.3), and Vercel AI SDK harnesses (CVE-2026-64650 / -64651, CVSSv4 6.3).

> ▸ This is NOT prompt injection. There is no probabilistic model to fool, and no 'smarter' model resists it, because authority is inferred from the SHAPE of the data rather than from provenance.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 0 -- The Normal Agent Loop (baseline)

In a healthy agent flow, the SDK sends the user request, system prompt, conversation history, and tool definitions to the model. The model decides whether to call a tool and returns a structured instruction naming the tool plus arguments. The SDK then dispatches it. The trust assumption is that the only producer of a tool-call block is the model itself.

#### PHASE 1 -- Provenance Gap Discovery

The researchers observed that the runtime does not verify provenance between 'model produced this' and 'dispatcher executes this.' The event loop treats any object shaped like a model-generated tool call as authoritative. The attacker's goal is therefore to place such an object where the loop consumes it.

#### PHASE 2 -- Reaching the Dispatch Path (redacted)

The concrete methods for smuggling a tool-use block into the consumed position differ per platform (final-message injection into an authenticated request; session-history event injection; resumable-event function_call parts; or a sandbox process-path spoof). The exact request shapes are withheld here.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Confirmation / Authorization Forgery (redacted)

Where a platform gates sensitive tools behind human confirmation, the flaw is that the confirmation processor did not check that the target tool belonged to the executing agent, actually required confirmation, or matched the recorded call. A forged approval could thus run an unauthorized tool. Exact forgery structure withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Impact: Credential & Data Exfiltration

Because the executed tool inherits the agent's full authority, the blast radius equals whatever the agent can already do: secret lookups, deployment operations, cloud API calls, file writes. An agent wired to no sensitive tools yields the attacker nothing; an over-privileged agent yields credentials and data egress. The researchers sent PoC to vendors and did not release it publicly.

### ▚ REAL-WORLD :: WHERE THIS LANDS

A CI/CD 'release agent' with a deploy tool and secret-manager read scope is the canonical target: an attacker who can shape conversation history or resumable events could drive a tool call that reads and ships credentials, with EDR seeing only a permitted process making a permitted network request. In finance, an agent that reconciles transactions and holds a payments API token is an equivalent prize. The lesson generalizes to any org standing up unattended agent automation.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Authorize at execution time: bind every tool invocation to the exact model event, tool name, arguments, session, and authorization state that produced it (one-time, short-lived authorization).

**[2]** Treat conversation history, resumable events, confirmation responses, and structured tool-use blocks as UNTRUSTED input the moment they cross an external boundary; build message history from your own application, not caller-shaped input.

**[3]** Patch: Google ADK for Python &gt;= 2.5.0; @ai-sdk/harness-codex &gt;= 1.0.29; @ai-sdk/harness-opencode &gt;= 1.0.28. AWS fixed the managed AgentCore server-side.

**[4]** Reduce inherited authority: give each agent only the tools, cloud roles, and write permissions its task strictly requires -- the flaw's impact is bounded by the agent's standing privilege.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Black Hat USA 2026 -- Session page (The CoreBreak Attack)**  
<https://blackhat.com/us-26/briefings/schedule/#the-corebreak-attack-turning-ai-agents-into-credentials-exfiltration-vectors-53825>

**The Hacker News -- AWS, Google, and Vercel Agent Flaws Let Attackers Trigger Tools Without Running the Model**  
<https://thehackernews.com/2026/08/aws-google-and-vercel-patch-agent-flaws.html>

**AWS Security Bulletin -- 2026-073 (CVE-2026-18830)**  
<https://aws.amazon.com/security/security-bulletins/2026-073-aws/>

</details>

---

## 0x04 :: Can AI Do Novel Security Research? Meet the HTTP Terminator

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 + DEF CON 34 |
| **TRACK** | AI // Web / HTTP Desync |
| **WHEN** | BH: Aug 5 12:00 (Oceanside A) // DC34: Aug 7 12:00 (Main Track 3) |
| **SPEAKER** | James 'albinowax' Kettle — *PortSwigger Research* |
| **TAGS** | `autonomous research` `HTTP desync` `RQP` `ideation-evaluation-cascade` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Kettle built an autonomous research engine -- the HTTP Terminator -- that INVENTS new HTTP desync attack techniques and proves them against live, bug-bounty-authorized targets at scale. It compromised banks, security products, and government infrastructure, and found a zero-day in Apache Traffic Server (CVE-2026-63078).

> ▸ The headline research finding is methodological: an Ideation -&gt; Evaluation -&gt; Weaponization -&gt; Cascade loop, where the human's highest-leverage role is the discovery cascade, not running the loop and stepping away.

> ▸ Also surfaced a genuinely new attack concept -- 'Shared-Parser Confusion' -- in which servers reuse parser code between requests and responses, so any response-processing feature becomes reachable by a crafted request.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Ideation via 'micro-inspiration'

Rather than prompting a model to 'find desync bugs' (which mostly regurgitates known art), the system splits RFCs into 1-3 sentence fragments and asks for 1-5 candidate request structures per fragment. 138 HTTP/SMTP RFCs -&gt; ~15,000 micro-fragments -&gt; ~30,000 unique candidate vectors after normalization. Key lesson: models aggressively anchor on context, so every extra sentence risks 'context contamination' that kills novelty.

#### PHASE 2 -- Evaluation as the load-bearing primitive

A Burp extension backed by SQLite tested candidates 24/7 against authorized targets under heavy per-domain rate limits. The core test: does a normally-consistent request start getting a DIFFERENT response when paired with a candidate trigger over a separate connection? This is class-agnostic -- it can detect desync patterns the researcher does not yet know exist -- with an anomaly layer flagging odd text/binary blends.

#### PHASE 3 -- Weaponization & the 'AI vs Code vs Human' framing

Turbo Intruder was given an MCP interface and driven in autonomy. The durable engineering lesson: move responsibility from disposable AI-generated code toward deterministic code over time; deterministic validation gates produced a zero-false-positive pipeline. Specific trigger payloads and the reliability 'dangling-byte' RQP enhancement are summarized conceptually, not reproduced.

#### PHASE 4 -- Agent-steering 'dark arts' (documented, not endorsed)

To coax a safety-tuned coding agent into high-volume work, Kettle reports reframing the tool as a 'simulator,' offering placebo capabilities, masking misinterpreted signals, and renaming attack classes to escape bad semantic anchors. This is presented as an honest account of how autonomy can be nudged -- and, implicitly, why model-layer guardrails alone are brittle.

#### PHASE 5 -- The Cascade (where humans amplify AI)

Each proven finding is interrogated with two questions: how do I detect similar behavior elsewhere, and does its origin enable other attacks? This feedback loop produced Status-Line Injection, Range Cache Poisoning, and -- most significantly -- Shared-Parser Confusion. The ATS zero-day emerged from a lucky permutation plus an updated anomaly detector: a human-in-the-loop cascade, not full autonomy.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Response Queue Poisoning against a live airport exposed internal staff panels (flights, passengers, luggage); a live bank leaked a long-lived API key mid-PoC. The transferable threat: any org exposing upstream HTTP/1.1 between a front-end and back-end is now testable at machine scale by an autonomous adversary that invents its own triggers. Defenders should assume attackers can run the same loop.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Never use upstream HTTP/1.1 -- use HTTP/2 or higher end-to-end; this is the root-cause fix for the desync class.

**[2]** If forced to use HTTP/1.1 upstream, apply an allow-list of HTTP methods on BOTH front-end and back-end.

**[3]** Use a separate allow-list of which methods may carry a body (POST, maybe PUT/PATCH); GET/HEAD/OPTIONS should never carry one.

**[4]** Adopt the same automation-first mindset defensively: fuzz your own edge with the open-sourced HTTP Request Smuggler updates before an autonomous adversary does.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**PortSwigger Research -- Can AI do novel security research? Meet the HTTP Terminator (whitepaper)**  
<https://portswigger.net/research/can-ai-do-novel-security-research>

**Black Hat USA 2026 -- Session page**  
<https://blackhat.com/us-26/briefings/schedule/#can-ai-do-novel-security-research-meet-the-http-terminator-51894>

**Printable whitepaper PDF**  
<https://portswigger.net/kb/papers/gkaicuremal/http-terminator.pdf>

</details>

---

## 0x05 :: When AI Attacks AI: Inside the Self-Propagating Botnet Built on Compromised AI Infrastructure

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | Threat Hunting & IR // AI, ML & Data Science |
| **WHEN** | Aug 6, 2026 ~10:15 AM PT |
| **SPEAKER** | Gal Elbaz & Avi Lumelsky — *Oligo Security* |
| **TAGS** | `Ray` `CVE-2023-48022` `ShadowRay 2.0` `compute-layer supply chain` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ The first documented in-the-wild campaign ('ShadowRay 2.0') weaponizing Ray clusters -- the compute backbone for much of the agent ecosystem -- into a self-propagating botnet: compromised clusters autonomously scan for and infect other Ray deployments globally.

> ▸ Rooted in CVE-2023-48022, which Ray maintainers characterize as a design feature for controlled environments; the researchers count 200,000+ exposed servers and a campaign active since 2024.

> ▸ Strategic point: if the compute layer is compromised, agent workloads may run on infrastructure that is already owned -- a supply-chain risk that is documented, not theoretical.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Exposure & Enumeration

Ray dashboards and job-submission endpoints exposed to the internet are discoverable at scale. The design decision that job submission implies code execution means a reachable cluster is, in effect, an execution surface.

#### PHASE 2 -- Foothold via CVE-2023-48022 (redacted)

The specific job-submission abuse that yields code execution on a worker is well documented publicly but withheld here in operational form; conceptually it converts 'submit a job' into 'run attacker code.'

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- AI-Assisted Payload Generation

Oligo assess that the campaign uses AI to generate malicious code, producing a self-sustaining malware ecosystem that adapts persistence and exclusivity logic (e.g., evicting rival miners). Exact payloads are not reproduced.

#### PHASE 4 -- Self-Propagation

Each compromised cluster becomes a scanner-and-infector for other Ray deployments, giving worm-like growth. Observed objectives include crypto-mining, data theft, and DDoS staging.

#### PHASE 5 -- Why It Matters for Agents

Because agent frameworks schedule work onto Ray, a poisoned cluster can taint model inference, training, or tool execution beneath an otherwise 'secure' agent. Endpoint controls at the app layer never see the compromise below them.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Enterprises running Ray for model training or agent orchestration on cloud GPUs are directly in scope; DeFi/quant shops running compute-heavy pipelines inherit the same exposure. The generalized threat is infrastructure-level compromise underneath application-level trust -- a blind spot for gateway-only defenses.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Never expose Ray dashboards or job-submission endpoints to untrusted networks; treat a reachable cluster as a remote code execution surface by design.

**[2]** Enforce network segmentation and strict egress control on compute clusters so a foothold cannot scan-and-spread or exfiltrate.

**[3]** Add authentication/authorization in front of Ray (proxy, mTLS, allow-lists); do not rely on the 'controlled environment' assumption in cloud deployments.

**[4]** Monitor for the behavioral signature of worming (outbound scans to peer clusters, unexpected miner processes) rather than for a single static IOC.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Forkast -- Black Hat USA 2026 Signals Agent Exploitation Has Become Its Own Infrastructure Discipline**  
<https://forkast.news/black-hat-usa-2026-signals-agent-exploitation-has-become-its-own-infrastructure-discipline/>

**Forkast -- Black Hat Day 1 Briefings Reveal the Agent Stack Is the Attack Surface**  
<https://forkast.news/black-hat-day-1-briefings-reveal-the-agent-stack-is-the-attack-surface/>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

</details>

---

## 0x06 :: No Tools Required: Post-Injection Exploitation Across AI Agent Frameworks

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // AppSec |
| **WHEN** | Aug 5, 2026 ~2:35 PM |
| **SPEAKER** | Yarden Porat & Shahar Tal — *Check Point Research* |
| **TAGS** | `LangChain` `CrewAI` `AutoGen` `Semantic Kernel` `framework runtime` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Reframes agent security from 'control the tools' to 'the framework itself is the vulnerability.' Exploitable logic lives in the core runtimes -- memory stores, planning loops, serialization layers, orchestration -- of LangChain, CrewAI, AutoGen, and Semantic Kernel.

> ▸ Even WITHOUT tool access, attacker-controlled content can cross trust boundaries and hijack agents through framework internals.

> ▸ Techniques include delayed-execution injection across conversation turns, cross-agent propagation in multi-agent setups, and persistent memory poisoning.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Map the Framework Trust Boundaries

The runtime, not just the tool layer, makes security decisions: what gets remembered, when a plan step fires, how objects are (de)serialized. Each is a boundary an attacker-influenced string can traverse.

#### PHASE 2 -- Delayed-Execution Injection (redacted)

Malicious content can be parked so it executes on a LATER conversation turn than the one that introduced it, defeating single-turn review. Concrete crafting is withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Persistent Memory Poisoning (redacted)

By writing crafted content into an agent's long-term memory store, an attacker influences future reasoning long after the injecting message scrolls out of context. Store-specific write techniques are withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Cross-Agent Propagation

In multi-agent systems, poisoned context handed from one agent to the next lets an effect propagate along the orchestration graph -- a lateral-movement analogue for agent meshes.

#### PHASE 5 -- Consequence for Defense Strategy

If the attack surface is the framework's decision-making logic rather than the tools it calls, then tool-permissioning, output filtering, and prompt guardrails are all addressing the wrong layer.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Any enterprise standing up multi-agent workflows on these popular frameworks inherits the exposure regardless of how tightly it scopes tools. A poisoned memory entry in a customer-support agent could steer responses days later; a compromised planner in a finance agent mesh could propagate to downstream agents that hold real authority.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Govern at the decision layer: instrument and constrain memory writes, plan-step execution, and inter-agent handoffs -- not just tool calls.

**[2]** Isolate and validate memory stores; treat retrieved memory as untrusted input subject to the same scrutiny as fresh user content.

**[3]** Segment multi-agent graphs so a poisoned upstream agent cannot silently grant authority to downstream agents.

**[4]** Prefer deterministic serialization with strict schemas over permissive object deserialization in the runtime.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Forkast -- Black Hat Day 1 Briefings Reveal the Agent Stack Is the Attack Surface**  
<https://forkast.news/black-hat-day-1-briefings-reveal-the-agent-stack-is-the-attack-surface/>

**Forkast -- Agent Exploitation Has Become Its Own Infrastructure Discipline**  
<https://forkast.news/black-hat-usa-2026-signals-agent-exploitation-has-become-its-own-infrastructure-discipline/>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

</details>

---

## 0x07 :: Cost-Effective, Private, Frontier-Grade: AI Agent Exploitation with a Fine-Tuned OSS Model

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Offensive |
| **WHEN** | Aug 6, 2026 ~10:15 AM PT |
| **SPEAKER** | Bar Lanyado & Eliya Cohen — *NVIDIA* |
| **TAGS** | `WASP-OS` `30B OSS model` `offensive economics` `private inference` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ A fine-tuned 30B open-source model ('WASP-OS') reached a 56% exploit success rate against AI agents -- edging out much larger frontier models (GPT-4o, Claude, Gemini class) -- at roughly 70-125x lower cost, with full privacy.

> ▸ The structural point is economic: when serious offensive capability no longer requires frontier API spend or exposes attack patterns to a cloud provider, the attacker's cost structure collapses while the defender's surface grows.

> ▸ A direct rebuttal to 'you need frontier scale to do serious offensive work,' and a signal of where purpose-trained offensive models are heading.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Task Framing

Exploitation of agents is decomposed into a repeatable task the model is tuned for, rather than a general capability -- narrow specialization beats breadth for this workload.

#### PHASE 2 -- Fine-Tuning Corpus (redacted)

The composition of the offensive fine-tuning dataset and training recipe is the core uplift and is withheld. Conceptually it aligns a mid-size OSS base toward the agent-exploitation task distribution.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Benchmarking vs Frontier

Measured success rate (56%) is reported as matching or exceeding frontier models on the same agent-exploitation benchmark, establishing capability parity at a fraction of cost.

#### PHASE 4 -- Cost & Privacy Economics

70-125x lower run cost and local (private) inference remove two frictions that previously kept the offensive barrier high: spend, and exposure of one's methods to a provider.

#### PHASE 5 -- Trajectory

Purpose-trained, self-hosted offensive models make scaled agent attacks accessible to far more actors -- the imbalance widens as every new agent deployment adds surface.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Lowered cost/privacy barriers mean red-team-grade agent exploitation is now reachable by mid-tier and criminal actors, not just well-funded labs. Defenders should assume adversaries can run capable offensive models locally and cheaply, and can iterate without leaving cloud telemetry.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Assume commodity, private offensive AI in your threat model; do not rely on the cost or scarcity of frontier access as a barrier.

**[2]** Invest in agent-side detection and least-privilege so exploit SUCCESS is bounded even when exploit ATTEMPTS are cheap and frequent.

**[3]** Continuously red-team your own agents with comparable tooling to find what a 56%-success adversary would find first.

**[4]** Track machine-identity sprawl (machine identities now vastly outnumber humans) as part of the growing surface these models target.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Forkast -- Agent Exploitation Has Become Its Own Infrastructure Discipline**  
<https://forkast.news/black-hat-usa-2026-signals-agent-exploitation-has-become-its-own-infrastructure-discipline/>

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

</details>

---

## 0x08 :: Bye Bye AI: How We Hacked the AI Shopping Assistant of a Top-3 US Retailer

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science |
| **WHEN** | Aug 5, 2026 10:15-10:45 AM PST |
| **SPEAKER** | Netanel Rubin & Dan Avraham — *Rein Security* |
| **TAGS** | `Vertex AI Search` `LLM gateway` `intent-classification bypass` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Rubin and Avraham compromised the AI shopping assistant of a top-3 US retailer -- a system built on Vertex AI Search sitting behind an LLM gateway meant to enforce intent-classification guardrails.

> ▸ Core lesson: gateway defenses that only watch prompts and responses miss the part that matters. Securing an AI agent requires visibility into what it actually EXECUTES, not just the text going in and out.

> ▸ A production case study of guardrail bypass against a real, high-traffic commerce agent.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Recon of the Assistant's Capabilities

Establish what the assistant can retrieve and do (search over catalog + backend actions) and where the intent-classification gateway sits relative to execution.

#### PHASE 2 -- Probing the Intent Gateway (redacted)

The gateway classifies requests as allowed/blocked by intent. The researchers found inputs that pass classification yet steer the assistant toward unintended behavior; concrete bypass phrasings are withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Gateway/Execution Gap

The decisive gap is between what the gateway inspects (prompt + response text) and what the agent actually executes against Vertex AI Search and backend services. Actions can diverge from the surface conversation.

#### PHASE 4 -- Impact

By exploiting that gap, the assistant can be driven to actions outside its intended shopping scope. Specific abuse chains against the retailer are generalized here rather than reproduced.

#### PHASE 5 -- Generalization

Any 'guardrail-in-front-of-agent' architecture that lacks execution visibility shares this weakness; the pattern is broader than one retailer.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Retail and e-commerce assistants that can touch order, account, or pricing backends are directly implicated. The same architecture -- an intent gateway wrapping an execution-capable agent -- appears across banking chat assistants and SaaS copilots, so the execution-visibility gap is an industry-wide pattern.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Instrument what the agent EXECUTES (tool calls, backend queries, actions), not just the prompt/response pair the gateway sees.

**[2]** Treat intent classification as one signal, never the sole control; enforce least-privilege on the backend actions the assistant can invoke.

**[3]** Add server-side authorization on every backend action so a steered assistant cannot exceed the user's actual entitlements.

**[4]** Log and alert on divergence between stated conversational intent and executed actions.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Black Hat USA 2026 -- Session page (Bye bye AI)**  
<https://blackhat.com/us-26/briefings/schedule/#bye-bye-ai-how-we-hacked-the-ai-shopping-assistant-of-a-top-3-us-retailer-53360>

**LastPass -- Complete Guide to Black Hat USA 2026**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

</details>

---

## 0x09 :: ChatMate: Remote Prompt Execution on AI Assistants through Sandbox Escaping

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Sandboxing |
| **WHEN** | Aug 6, 2026 10:15-10:45 AM PST |
| **SPEAKER** | Ori Lahav — *Rubrik Zero Labs* |
| **TAGS** | `Remote Prompt Execution` `Copilot sandbox escape` `one-document trigger` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Introduces 'Remote Prompt Execution' (RPE) -- a class where, much like remote code execution, an attacker runs arbitrary PROMPTS inside a victim's AI chat session.

> ▸ The chain culminates in what is described as the first demonstrated escape from the Copilot sandbox to the host underneath it -- a full session takeover triggered by uploading a single document.

> ▸ Blast radius spans several Azure services, illustrating that an assistant sandbox escape is a cloud-tenancy problem, not just a chat problem.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Weaponized Document (redacted)

A single uploaded document carries content that the assistant processes; the specific crafting that converts 'summarize this' into attacker-controlled prompt execution is withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 2 -- Remote Prompt Execution

Once the document is processed, the attacker effectively injects prompts into the victim's authenticated session -- controlling the assistant's behavior as if they were the user.

#### PHASE 3 -- Sandbox Escape (redacted)

The novel step is escaping the assistant's sandbox to the host. Mechanism detail is withheld; conceptually it breaks the isolation boundary the sandbox is supposed to guarantee.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Session Takeover & Lateral Reach

Host access yields full session takeover with reach across several connected Azure services -- the assistant becomes a pivot into the surrounding cloud tenant.

#### PHASE 5 -- Class Generalization

RPE reframes assistant security: if untrusted content can execute prompts and then break the sandbox, the assistant is an initial-access vector into the host and cloud.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Enterprise Copilot-style assistants that ingest user documents and run in cloud sandboxes are the archetype. A single malicious attachment mailed to a target -- or shared in a workspace -- becomes an initial-access primitive with cloud blast radius, which is squarely a corporate IR concern.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Harden the assistant sandbox as a genuine security boundary; assume untrusted documents will attempt escape and test accordingly.

**[2]** Constrain the assistant's host and cloud permissions so an escape yields minimal lateral reach (least privilege across connected services).

**[3]** Treat uploaded documents as untrusted executable input, not passive data; scan and isolate processing.

**[4]** Monitor assistant-originated activity against connected cloud services for anomalies indicating a pivot.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Black Hat USA 2026 -- Session page (ChatMate)**  
<https://blackhat.com/us-26/briefings/schedule/#chatmate-remote-prompt-execution-on-ai-assistants-through-sandbox-escaping-52326>

**LastPass -- Complete Guide to Black Hat USA 2026**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

</details>

---

## 0x0A :: Caging the Agent: How Roblox Built Multi-Layer Sandboxes to Secure Claude Code at Enterprise Scale

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Defense |
| **WHEN** | Aug 5-6, 2026 |
| **SPEAKER** | Roblox security engineering — *Roblox* |
| **TAGS** | `defensive architecture` `coding-agent containment` `EDR blind spot` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ A DEFENSIVE case study: after a hidden instruction inside a GitHub Issue convinced Claude Code to upload Roblox credentials to a public repo -- in an internal testing environment -- Roblox built layered containment around coding agents.

> ▸ The chilling detail: EDR saw nothing, because there was nothing anomalous to see. A permitted process made a permitted network request. This is the coding-agent blind spot in one sentence.

> ▸ The build-out: sandboxes for macOS, Linux, Windows, and cloud VMs; a gateway in front of the model; managed system prompts; VPN profiles that cut production access entirely; and 23+ documented penetration-test findings.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Incident

An indirect prompt injection hidden in a GitHub Issue drove the coding agent to exfiltrate credentials to a public repository. The injection arrived inside ordinary developer content the agent was expected to read.

#### PHASE 2 -- Why EDR Was Blind

The exfil used a permitted process making a permitted request -- no malware, no anomalous binary, no unusual destination category. Endpoint detection keyed on 'anomalous' had nothing to fire on.

#### PHASE 3 -- Multi-Layer Sandboxing

Roblox built OS-native sandboxes across macOS/Linux/Windows plus cloud VMs to contain what the agent can touch, so a hijack cannot reach production secrets or systems.

#### PHASE 4 -- Gateway + Managed Prompts + Network Policy

A gateway in front of the model, centrally managed system prompts, and VPN profiles that sever production access reduce blast radius at the network and policy layers rather than trusting the model to behave.

#### PHASE 5 -- Validation

The resulting architecture was pen-tested, yielding 23+ findings -- underscoring that containment is iterative and that even a layered cage needs adversarial validation.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Every enterprise rolling out Claude Code / Cursor / Copilot-style coding agents faces the same blind spot: a permitted agent process doing a permitted thing on behalf of a hidden instruction. Roblox's layered cage (sandbox + gateway + network cutoff) is a directly transferable blueprint for regulated environments.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Do not rely on EDR to catch agent exfil: a permitted process doing permitted I/O is invisible to anomaly-based detection. Contain, don't just detect.

**[2]** Sandbox coding agents at the OS/VM layer so a hijacked agent cannot reach production credentials or systems.

**[3]** Put a gateway in front of the model and centrally manage system prompts; sever production network access with VPN/egress policy by default.

**[4]** Treat inbound developer content (issues, PRs, comments, repo files) as untrusted injection surface; pen-test the cage continuously.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Forkast -- From Lab Curiosity to Mainstream Threat: Black Hat USA 2026 and the Rise of AI Agent Security**  
<https://forkast.news/from-lab-curiosity-to-mainstream-threat-black-hat-usa-2026-and-the-rise-of-ai-agent-security/>

**Black Hat USA 2026 -- Session page (Caging the Agent)**  
<https://blackhat.com/us-26/briefings/schedule/#caging-the-agent-how-roblox-built-multi-layer-sandboxes-to-secure-claude-code-at-enterprise-scale-53708>

**CVE-2026-25725 -- Claude Code sandbox escape via settings.json (context)**  
<https://osv.dev/vulnerability/CVE-2026-25725>

</details>

---

## 0x0B :: A Billion-User Blast Radius: Owning ChatGPT's Secure Sandbox

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 + DEF CON 34 |
| **TRACK** | Cloud Security // AI Sandboxing |
| **WHEN** | BH: Aug 5, 2026 // DC34: Aug 9 10:00 AM (Creator Stage 5) |
| **SPEAKER** | Simcha Kosman — *Palo Alto Networks* |
| **TAGS** | `ChatGPT sandbox` `LLM-supervisor bypass` `shared-backend C2` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ A proof-of-concept chain claiming full command-and-control inside ChatGPT's isolated sandbox -- bypassing the LLM supervisor to achieve persistent root execution.

> ▸ Demonstrated tricking a victim's ChatGPT into running attacker-controlled code in its sandbox, using that code to influence future reasoning, and abusing a shared backend to pass data from the victim's sandbox to the attacker's.

> ▸ OpenAI states the specific component was removed prior to the talk and, in its view, the work is not a sandbox escape or cross-account access -- the PoC value is in what a container sandbox failing WOULD mean at billion-user scale.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Getting Code Into the Sandbox (redacted)

The victim's ChatGPT is induced to execute attacker-controlled code inside its own sandbox. The inducement technique is withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 2 -- Supervisor Bypass (redacted)

The chain reportedly bypasses the LLM supervisor that is meant to constrain sandbox behavior, reaching persistent root execution. Mechanism withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Influencing Future Reasoning

Code in the sandbox is used to shape the model's subsequent reasoning -- turning a one-time execution into durable behavioral influence.

#### PHASE 4 -- Shared-Backend C2

A shared backend is abused as a covert channel so data flows from the victim's sandbox to the attacker's own sandbox -- command-and-control between tenants of the same service.

#### PHASE 5 -- Scale Framing

At a billion users, even a low-probability container weakness has enormous aggregate blast radius; the PoC is a call to treat consumer-AI sandboxes as serious multi-tenant boundaries.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Consumer and enterprise ChatGPT usage that runs code (data analysis, file handling) depends on that container boundary. The transferable concern is any shared-backend AI service where a sandbox weakness could bridge tenants -- a multi-tenant isolation problem familiar from cloud, now applied to AI runtimes.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Vendors: treat AI code sandboxes as hostile multi-tenant boundaries; minimize shared-backend channels that could bridge sandboxes.

**[2]** Do not rely on an LLM 'supervisor' as the primary isolation control; enforce isolation in the container/host layer.

**[3]** Enterprises: constrain what data enters AI code-execution features, since sandbox contents are the blast radius.

**[4]** Monitor for cross-session data influence patterns and unexpected persistence inside ephemeral sandboxes.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Dark Reading -- Researcher Claims Control of ChatGPT Secure Sandbox**  
<https://www.darkreading.com/cloud-security/researcher-claims-control-chatgpt-secure-sandbox>

**DEF CON 34 -- Creator Stage Talks listing**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**Black Hat USA 2026 -- Session page**  
<https://blackhat.com/us-26/briefings/schedule/#a-billion-user-blast-radius-owning-chatgpts-secure-sandbox-53432>

</details>

---

## 0x0C :: Pwning Agentic Browsers with PleaseFix: A New Vulnerability Class for 0-Click Takeover

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 (AI Village track) + Black Hat USA 2026 |
| **TRACK** | AI Village // Creator Stage 3 |
| **WHEN** | DC34: Aug 9 12:00-12:30 PM (Creator Stage 3) |
| **SPEAKER** | Michael Bargury & Stav Cohen — *Zenity Labs* |
| **TAGS** | `agentic browser` `indirect prompt injection` `Intent Collision` `same-origin break` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ 'PleaseFix' is a CLASS of zero-click attacks against agentic browsers (Perplexity Comet, Claude in Chrome, and others): malicious instructions placed in content the agent is already expected to read (emails, calendar invites, web pages) hijack the agent against its own user -- no click, no download, no user awareness.

> ▸ The named technique is 'Intent Collision': hidden instructions interfere with the user's legitimate request and redirect the agent to act on the attacker's behalf using the user's own identity, permissions, and access.

> ▸ Agentic browsers reason across multiple sources in one session, which fundamentally BREAKS the same-origin principle -- a ~20-year regression in the browser security model. Demonstrated chains reach file exfiltration, credential theft, and full account takeover (incl. an integrated password manager).

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Deliver the Poisoned Content (redacted)

A weaponized artifact (e.g., a calendar invite indistinguishable from a real one) is delivered. Attacker instructions are hidden within content the agent will read during an ordinary task. Concealment specifics are withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 2 -- Intent Collision

When the user asks the agent to do something routine ('accept this meeting,' 'summarize this email'), the hidden instructions collide with the legitimate intent and steer the agent -- while it still returns the expected result to the user, masking the compromise.

#### PHASE 3 -- Same-Origin Collapse

Because the agent reasons across trusted and untrusted sources within one authenticated session, it cannot reliably distinguish them. Untrusted content gains the agent's authority -- the structural failure behind the class.

#### PHASE 4 -- Action Under User Identity (redacted)

The agent performs sensitive actions (local file read/exfil; authenticated workflow abuse against a password manager) using the user's identity. Exact chains are withheld; e.g., with Claude in Chrome the agent's own javascript tool was turned into XSS-as-a-service on any visited site.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 5 -- Impact

Demonstrated outcomes: Gmail exfiltration, silent Google Drive sharing, and takeover of Slack/X/Claude accounts from a single malicious email; file-system exfil and credential/account takeover on Comet.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Anyone running an agentic browser inside an authenticated session -- with email, files, calendar, and connected SaaS -- is exposed to a single crafted message. For enterprises, one poisoned calendar invite or email can pivot into Drive, Slack, and identity provider access, which existing browser/endpoint controls were never designed to see (agent-to-service traffic, not human-to-service).

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Reduce blast radius with governance: scope OAuth grants tightly and limit what connected services an agentic browser can reach.

**[2]** Verify vendor patch status for any deployed agentic browser; the class implicates any product with broad OAuth authorization plus autonomous processing of fetched content.

**[3]** Require human confirmation for sensitive agent actions (file access, sharing, credential-store interaction) -- do not let routine tasks auto-execute them.

**[4]** Treat agent-to-service activity as a new monitoring domain; conventional DLP/EDR watch human&lt;-&gt;system traffic, not autonomous agent&lt;-&gt;service traffic.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Zenity Labs -- PleaseFix: Zero-Click AI Agent Vulnerabilities**  
<https://zenity.io/research/pleasefix-vulnerabilities>

**Dark Reading -- AI Browsers Vulnerable to 'PleaseFix' Zero-Click Agent Hijacking**  
<https://www.darkreading.com/cyber-risk/ai-browsers-zero-click-agent-hijacking>

**DEF CON 34 AI Village -- Schedule**  
<https://aivillage.org/events/defcon-34/>

</details>

---

## 0x0D :: Pwning the Internet of Agents: Zero-Click Backdoors in OpenClaw and a Global Agent Botnet on MoltBook

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 (AI Village fireside) |
| **TRACK** | AI Village // W603 Fireside |
| **WHEN** | Aug 7, 2026 3:00-4:00 PM |
| **SPEAKER** | Stav Cohen & Joao Maria Campos Donato — *Zenity* |
| **TAGS** | `Internet of Agents` `zero-click backdoor` `agent-to-agent worm` `connected ecosystems` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ As agents connect to one another, a compromise in one can spread through the ecosystem: this session covers zero-click backdoors in a connected coding-agent platform (OpenClaw) and a demonstrated global agent botnet (on 'MoltBook').

> ▸ The unifying idea: the 'Internet of Agents' inherits worm dynamics -- backdoors and malicious context can propagate agent-to-agent without a human in the loop.

> ▸ Pairs with AI Village poster research on MCP-based agent-to-agent worm propagation and malicious-context spread, indicating a coherent new threat family.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Connected-Agent Attack Surface

Agents wired to other agents, marketplaces, and shared context stores form a reachable graph. A single compromised node has many neighbors.

#### PHASE 2 -- Zero-Click Backdoor (redacted)

A backdoor is planted without user interaction via content the agent processes in normal operation. Specific implant crafting is withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Agent-to-Agent Propagation

The backdoor/malicious context spreads from one agent to the next along the connection graph -- worm-like growth without human clicks (mirrored by MCP tool-poisoning worm research in the poster track).

#### PHASE 4 -- Botnet Assembly

Propagated implants coordinate into a global agent botnet, giving an attacker distributed control over many agents and their delegated authority.

#### PHASE 5 -- Systemic Consequence

Because each agent carries real user/enterprise authority, an agent botnet is a distributed authority-abuse platform, not merely spare compute.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Organizations adopting connected agent ecosystems, MCP servers, and agent marketplaces face genuine worm risk: one poisoned skill or context source can cascade across an internal agent fleet. This is the agentic analogue of classic network worms, now operating over agent-to-agent trust rather than TCP/IP.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Isolate agents and constrain agent-to-agent trust; do not let one agent silently inject context or tools into another.

**[2]** Vet and pin third-party skills / MCP servers; monitor for tool-poisoning and malicious-context propagation between agents.

**[3]** Contain blast radius so a compromised agent cannot reach the whole fleet (segmentation for agents, as for networks).

**[4]** Watch for worming behavior (unexpected agent-to-agent connections, context writes, mass identical actions) rather than single static indicators.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**DEF CON 34 AI Village -- Schedule & Fireside Chats**  
<https://aivillage.org/events/defcon-34/>

**AI Village Poster -- Agent-to-Agent Worm Propagation in MCP-Based AI Systems**  
<https://aivillage.org/posters/agent-to-agent-worm-propagation-in-mcp-based-ai-systems/>

**AI Village @ DEF CON 34 -- overview**  
<https://aivillage.org/events/defcon-34/>

</details>

---

## 0x0E :: Keynote Panel: What is the Right Balance of Rules for Defenders & Adversaries?

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 (AI Village) |
| **TRACK** | Main Track 1 // Keynote |
| **WHEN** | Aug 7, 2026 1:30-3:00 PM |
| **SPEAKER** | Bruce Schneier; Jason Clinton (Anthropic); Heather Adkins (Google); Emanuel Gawrieh (Google, AIV Co-Chair) — *AI Village* |
| **TAGS** | `dual-use policy` `offense-defense balance` `governance` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ A policy keynote on the central dual-use question of the year: does restricting AI capability protect defenders, or simply hand attackers the advantage?

> ▸ Frames the whole conference's offense/defense split from three angles -- policy (Schneier), product safety (Anthropic), and large-scale defense (Google).

> ▸ Sets the strategic context for the technical talks: as autonomous capability commoditizes, the governance question is no longer academic.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Framing the Dual-Use Dilemma

The same agentic capabilities that empower defenders (autonomous triage, scaled research) empower attackers (autonomous exploitation). Restriction has costs on both sides.

#### PHASE 2 -- The Policy View

Schneier situates the debate in decades of security-policy history: restriction, disclosure norms, and who benefits from friction.

#### PHASE 3 -- The Product-Safety View

Anthropic's perspective on shipping capable models with safeguards -- and the trade-offs of conservative controls that sometimes catch benign use.

#### PHASE 4 -- The Defender-at-Scale View

Google's vantage on defending billions of users and whether capability limits help or hinder that mission.

#### PHASE 5 -- Synthesis

No clean resolution: the panel maps the trade-space so practitioners can reason about their own posture rather than prescribing one rule.

### ▚ REAL-WORLD :: WHERE THIS LANDS

For a security leader, the panel is a decision framework: how to weigh capability adoption vs restriction in your own org, and how coming policy may shape access to both offensive and defensive AI. Directly relevant to anyone setting AI usage policy under regulatory pressure.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Build an explicit dual-use policy for AI capability in your org rather than defaulting to ad-hoc decisions.

**[2]** Assume adversary access to capable AI regardless of vendor restrictions; plan defense on that basis.

**[3]** Engage with disclosure and governance norms as a participant, since community effort -- not any single control -- shapes outcomes.

**[4]** Revisit posture as policy evolves; treat the offense/defense balance as a moving target.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**DEF CON 34 AI Village -- Schedule (Keynote Panel)**  
<https://aivillage.org/events/defcon-34/>

**AI Village @ DEF CON 34 -- overview**  
<https://aivillage.org/events/defcon-34/>

**Tech Times -- DEF CON 34 Opens: AI Agents Graduate From Novelty to Standard Hacking Weapon**  
<https://www.techtimes.com/articles/323346/20260806/def-con-34-opens-today-ai-agents-graduate-novelty-standard-hacking-weapon.htm>

</details>

---

## 0x0F :: HalCTF: Hostile Autonomous Layer CTF (+ the Autonomous-Agent Competition Arc)

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 (AI Village) |
| **TRACK** | AI Village // Competition |
| **WHEN** | Aug 7-9, 2026 (village hours) |
| **SPEAKER** | AI Village organizers — *AI Village* |
| **TAGS** | `autonomous pentesting` `agent-only CTF` `benchmark` `HAL` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ HalCTF is an agentic security competition where you NEVER touch the targets -- your autonomous agent does. Build an agent, package it as an OCI container, and deploy it against sandboxed challenges; all inference runs through a central service so nobody wins on GPU budget.

> ▸ It formalizes autonomous pentesting as a benchmark and marks the year autonomous agents shifted from novelty to standard competition weapon at DEF CON.

> ▸ Sits alongside 'AI Village Plays Pokemon' (novice-friendly local-model tooling) and a poster track documenting where autonomous agent security actually breaks.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Agent as Contestant

Entrants build an autonomous agent and containerize it (OCI). The human designs the loop; the agent executes against challenges unattended.

#### PHASE 2 -- Centralized Inference

All model inference is routed through a central service, neutralizing compute advantage and isolating the variable of interest: agent design, not hardware.

#### PHASE 3 -- Sandboxed Challenge Execution

Agents attack sandboxed targets; the harness measures autonomous capability on a level field -- effectively a benchmark for offensive agents.

#### PHASE 4 -- Human/AI Gap Measurement

Organizers note the best human teams remain stronger, but the gap has narrowed enough that competition architecture now assumes autonomous agents will compete.

#### PHASE 5 -- Research Output

Results and the accompanying poster track (runtime detection, SOC workflows, automated red teaming, human-oversight studies) feed back into defensive design.

### ▚ REAL-WORLD :: WHERE THIS LANDS

HalCTF is a preview of autonomous pentesting as a repeatable capability. For practitioners, it signals that offensive agents are now benchmarkable and improving -- and that defensive programs should adopt equivalent autonomous red-teaming to keep pace. The competition's design choices (containerized agents, central inference) are a template for internal agent evaluation.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Stand up autonomous red-teaming internally; treat offensive agents as a standing capability to benchmark against, not a curiosity.

**[2]** Study the AI Village poster track (runtime detection, unauthorized-tool-call detection, human rubber-stamping in oversight) for defensive patterns.

**[3]** Measure your own human-oversight quality: research here shows reviewers often 'press 1' to approve without real verification.

**[4]** Assume autonomous agents will find the easy findings first; fix those before an agent enumerates them.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**AI Village -- HalCTF: Hostile Autonomous Layer CTF**  
<https://aivillage.org/blog/halctf/>

**Tech Times -- DEF CON 34 Opens: AI Agents Graduate From Novelty to Standard Hacking Weapon**  
<https://www.techtimes.com/articles/323346/20260806/def-con-34-opens-today-ai-agents-graduate-novelty-standard-hacking-weapon.htm>

**AI Village @ DEF CON 34 -- Schedule**  
<https://aivillage.org/events/defcon-34/>

</details>

---

## VOLUME II :: HARNESSES, BROWSERS &amp; THE DISCOVERY ECONOMY

> Volume II goes deeper into the layer most organizations never security-review: the HARNESS that translates model intent into privileged action. It covers AI browser defense-in-depth failures, trust-handoff breaks across Claude Code / Gemini CLI / Codex, the pre-task attack surface that exists before the model ever runs, a comparative teardown of agent sandboxes, LLM-guided firmware discovery, defensive benchmarking of AI investigators, a new neural-traffic defensive layer, and the cluster of talks compressing the entire vulnerability lifecycle.

---

## 0x10 :: Attacking and Defending AI Browsers

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // AppSec |
| **WHEN** | Aug 5, 2026 -- Mandalay Bay |
| **SPEAKER** | Artem Chaikin — *Brave Software* |
| **TAGS** | `indirect prompt injection` `Opera / Comet / Atlas` `sentinel model` `defense-in-depth` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ EVERY AI browser Chaikin analyzed proved vulnerable to indirect prompt injection -- demos landed against Opera's AI browser, Perplexity Comet, and ChatGPT Atlas, leading to data exfiltration and account takeover.

> ▸ Atlas is the important case: it stacks system-level prompting, trusted/untrusted content tagging, secondary-model tool scanning, AND user approval prompts -- and was still bypassed. No single guardrail is sufficient.

> ▸ The honest conclusion: there is currently NO known perfect solution to prompt injection in AI browsers. Every mitigation helps; none guarantees. Chaikin's closing note was that the field has to 'deal with the uncertainty.'

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Structural Problem

AI browsers embed assistants that navigate and act on web applications on the user's behalf. Any page the agent reads becomes an instruction channel. This is the same trust collapse seen elsewhere in the agentic stack, but delivered through ordinary web content.

#### PHASE 2 -- Concealment Channels (redacted)

Demonstrated hiding places for attacker instructions included content concealed behind HTML (Opera), near-invisible text overlaid on an image (Comet), and text tucked inside a Reddit comment behind spoiler tags (Comet). Exact crafting is withheld; the transferable point is that ANY rendering trick that hides text from a human but not from the model is an injection channel.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Defeating Layered Guardrails (redacted)

Against Atlas, three distinct weaknesses were shown: trusted-content tags could be MIMICKED by attacker-supplied page content to confuse the model; exfiltration data hidden in URL fragments was not properly scanned by the tool-call scanner; and free users hitting usage caps could be silently downgraded to a weaker model that is more susceptible to injection. Chaikin's wry framing: 'is this some kind of pay-to-live scenario?' Operational specifics withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- The Model-Downgrade Insight

The downgrade finding deserves separate emphasis: security posture became a function of BILLING STATE. A capacity or cost decision silently changed the browser's resistance to attack -- an availability/economics control that turned into a security control without anyone designing it that way.

#### PHASE 5 -- Building the Defense (Brave's answer)

Having broken everyone else's, Chaikin had to defend his own employer's browser. Brave's approach: separate browser profiles so personal accounts are logged out by default; a hard floor on model capability (no downgrade below Claude Haiku 4.5); and language-based alignment checking. The alignment check -- inspired by Meta's Prompt Firewall concept -- pauses a tool action before execution while a second 'sentinel' model compares the user's original request, prior context, and the proposed action, then surfaces risk to the user. If you asked for a page summary and the agent decides to open Gmail, the sentinel flags the mismatch.

### ▚ REAL-WORLD :: WHERE THIS LANDS

This is the consumer-and-enterprise browser most people will actually use. A single crafted page, image, or forum comment can drive exfiltration or account takeover with no user error beyond 'browsing.' For enterprises the sting is the downgrade finding: your security posture may silently change based on plan tier or capacity, which no procurement checklist currently asks about.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Assume no single guardrail holds; layer system prompts, content tagging, tool-call scanning, human-in-the-loop, and a sentinel/verifier model -- and still assume residual risk.

**[2]** Set a hard MINIMUM model capability for security-relevant paths; never let cost or capacity silently downgrade the model behind an agent.

**[3]** Isolate identity from agency: separate browser profiles, logged-out-by-default personal accounts, and dynamic permissions scoped to the specific requested task.

**[4]** Scan the whole outbound surface, including URL fragments -- exfiltration hides in the parts of a request people forget to inspect.

**[5]** Adopt intent-alignment checking: pause the tool call and ask whether the proposed action matches the user's original request before executing.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Dark Reading -- No Perfect Fix for AI Browser Prompt Injection Flaws**  
<https://www.darkreading.com/application-security/no-perfect-fix-ai-browser-prompt-injection-flaws>

**Black Hat USA 2026 -- Session page (Attacking and Defending AI Browsers)**  
<https://blackhat.com/us-26/briefings/schedule/#attacking-and-defending-ai-browsers-51657>

**Dark Reading -- AI Agents Undermine Progress in Browser Security**  
<https://www.darkreading.com/application-security/ai-agents-undermine-progress-browser-security>

</details>

---

## 0x11 :: Trusted Enough to Run: Breaking AI Agents in Official Workflows

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Supply Chain |
| **WHEN** | Aug 5, 2026 3:35-4:15 PM PST (Mandalay Bay H, Level 2) |
| **SPEAKER** | Elad Meged — *Novee Security* |
| **TAGS** | `trust handoff` `harness security` `Claude Code / Gemini CLI / Codex` `supply chain` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ A trust-HANDOFF failure class in official AI-agent workflows: one internal stage marks attacker-influenced state as 'safe,' and a later stage consumes it with GREATER authority than the original check ever accounted for -- reaching remote code execution in some cases.

> ▸ Confirmed across Anthropic's Claude Code, Google's Gemini CLI, and OpenAI's Codex. Per Anthropic's own analysis, the exposure includes the runner's repository token and any workflow-injected secrets; per Google's analysis, these are categorized as supply chain compromises.

> ▸ The thesis names the neglected layer directly: the HARNESS. Models ship with built-in safeguards, but the harness translating model intent into action runs without humans in the loop -- so oversights there become unintentional risk.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Unattended Automation as the Premise

Official agent workflows increasingly run as trusted, unattended automation (CI/CD, scheduled jobs, bots reacting to repo events). No human reviews each step, so an internal 'this is safe' decision is final in practice.

#### PHASE 2 -- Mapping Internal Stages

These workflows are built from stages that each decide what is approved, sanitized, and safe to reuse. The researcher's method is to enumerate those stages and identify where one stage's guarantee is consumed by another.

#### PHASE 3 -- The Trust-Handoff Break (redacted)

The flaw is a semantic mismatch: stage A validates state under one set of assumptions; stage B interprets that same state more powerfully. Attacker-influenced data thereby crosses from 'checked' to 'executed.' Concrete handoff abuse is withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Outcomes

Demonstrated consequences span command execution, secret exposure, persistence, and policy bypass -- with vendor analyses framing the impact as supply chain compromise because the compromised workflow feeds downstream artifacts.

#### PHASE 5 -- The Generalizable Method

Meged's transferable guidance: find the gaps between VALIDATION and EXECUTION, and harden the points where trusted data becomes dangerous. That question applies to any agent harness, not just these three products.

### ▚ REAL-WORLD :: WHERE THIS LANDS

This is the single most directly applicable talk for anyone running coding agents in CI/CD. A repo-event-triggered agent with a runner token is the exact shape of the vulnerable pattern -- and it pairs precisely with the Roblox incident (0x0A), where a hidden instruction in a GitHub Issue produced credential exfiltration that EDR could not see. Same blind spot, approached from opposite ends.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Audit every stage boundary in your agent workflows: what does each stage GUARANTEE, and does the next stage assume more than that guarantee provides?

**[2]** Never let 'sanitized/approved' state gain authority as it moves downstream; re-validate at the point of execution under the executing stage's assumptions.

**[3]** Scope runner tokens and workflow secrets to the minimum; assume any agent workflow reachable by attacker-influenced input can expose them.

**[4]** Treat the harness as in-scope for security review -- model guardrails do not cover the code that translates model intent into privileged action.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**GlobeNewswire -- Novee Researchers to Present Four Sessions across Black Hat USA and DEF CON**  
<https://www.globenewswire.com/news-release/2026/07/28/3334295/0/en/Novee-Researchers-to-Present-Four-Sessions-across-Black-Hat-USA-and-DEF-CON-Uncovering-Vulnerabilities-in-Anthropic-OpenAI-and-Google.html>

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Dark Reading -- AI Harnesses Burst With Potential Exploit Opportunities**  
<https://www.darkreading.com/application-security/ai-harnesses-potential-exploit-opps>

</details>

---

## 0x12 :: No Prompt Required: Pre-Task RCE in Google Gemini CLI

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 |
| **TRACK** | Exhibit Hall West 3 - 906 |
| **WHEN** | Aug 9, 2026 10:00-10:30 AM |
| **SPEAKER** | Elad Meged — *Novee Security* |
| **TAGS** | `pre-task attack surface` `CVSS 10.0` `headless CI/CD` `config/env inputs` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ There is an attack surface that exists BEFORE an AI model processes its first task. Agents accept configuration files, environment variables, and other startup inputs before prompt-time safeguards ever activate.

> ▸ Flagship case: a DETERMINISTIC exploit in Google's Gemini CLI that Google's own security team scored CVSS 10.0 (since patched). It requires NO model interaction whatsoever -- no prompt, no injection, no persuasion.

> ▸ In headless CI/CD environments those startup inputs may be trusted automatically and can reach execution BEFORE the sandbox even starts -- meaning the containment you rely on isn't running yet when the attack lands.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Identify Pre-Task Inputs

Enumerate everything the agent consumes at startup: config files, environment variables, project-level settings, and other initialization state. These are inputs no prompt filter or model guardrail ever sees.

#### PHASE 2 -- Determine Authority Per Input

For each input, ask what authority it carries. Some merely set preferences; others can designate executables, alter paths, or disable protections. The high-authority ones are the targets.

#### PHASE 3 -- Reaching Execution Before the Sandbox (redacted)

The decisive question is whether that authority can reach execution or disable security controls before containment initializes. In the Gemini CLI case this produced deterministic RCE. Mechanism withheld; the CVE is vendor-patched.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Why Headless CI/CD Amplifies It

In unattended pipelines, startup inputs are frequently trusted by default and there is no human to notice anomalous initialization. Determinism matters here: unlike prompt injection, this fires every time, with no model-behavior variance.

#### PHASE 5 -- Methodology Takeaway

The reusable method: identify pre-task inputs, determine the authority each one carries, and test whether that authority can reach execution or switch off controls. Applies to any agent CLI, not just Gemini.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Any org running agent CLIs inside build pipelines is exposed to the pattern: a poisoned config file committed to a repo, or an environment variable set by a compromised earlier pipeline stage, can achieve execution without ever talking to the model. Because it's deterministic and model-independent, it is far more reliable for an attacker than prompt injection -- and invisible to every defense aimed at prompts.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Inventory and lock down agent startup inputs: config files, env vars, and project settings must be treated as privileged, integrity-protected artifacts.

**[2]** Verify your sandbox starts BEFORE any untrusted input is consumed -- containment that initializes late provides no protection at initialization time.

**[3]** In CI/CD, do not auto-trust pipeline-supplied configuration for agents; pin and validate it as you would a dependency.

**[4]** Patch Gemini CLI to the fixed version, and apply the same pre-task audit methodology to every other agent CLI you deploy.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**GlobeNewswire -- Novee Researchers to Present Four Sessions across Black Hat USA and DEF CON**  
<https://www.globenewswire.com/news-release/2026/07/28/3334295/0/en/Novee-Researchers-to-Present-Four-Sessions-across-Black-Hat-USA-and-DEF-CON-Uncovering-Vulnerabilities-in-Anthropic-OpenAI-and-Google.html>

**DEF CON 34 -- Creator Stage / Talk listings**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**Novee Security -- Labs & research index**  
<https://novee.security/blog/category/novee-labs/>

</details>

---

## 0x13 :: The Sandbox Is a Suggestion: Deconstructing AI Agent Sandboxes

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 |
| **TRACK** | Exhibit Hall West 3 - 1006 |
| **WHEN** | Aug 7, 2026 4:00-5:00 PM |
| **SPEAKER** | Elad Meged — *Novee Security* |
| **TAGS** | `containment comparison` `Claude Code / Gemini CLI / Codex CLI` `design-gap failures` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ A comparative teardown of the containment systems in Anthropic's Claude Code, Google's Gemini CLI, and OpenAI's Codex CLI. Each enforces differently -- and each rests on a structural assumption the runtime can violate.

> ▸ Critically, these containment mechanisms fail through DESIGN GAPS, not through prompt injection or model persuasion. The model is not the weak link here.

> ▸ Delivers a reusable evaluation methodology for ANY agent sandbox: (1) understand what it claims to enforce, (2) identify the assumption behind that enforcement, (3) test whether the real execution path breaks it.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Establish the Claim

For each product, document precisely what the sandbox says it enforces -- filesystem scope, network egress, process spawning, credential access. Claims differ substantially across the three.

#### PHASE 2 -- Surface the Hidden Assumption

Every enforcement mechanism rests on an assumption (e.g., that a given file exists at startup, that a path cannot be redirected, that a config is immutable). Naming that assumption is the core analytic move of the talk.

#### PHASE 3 -- Test the Real Execution Path (redacted)

Compare the assumption against what the runtime actually permits. Where the real execution path can violate the assumption, containment fails by design rather than by exploit cleverness. Product-specific break paths are withheld.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Cross-Product Comparison

The comparative framing is the value: three vendors, three enforcement philosophies, one shared weakness pattern. Choosing a different vendor does not escape the class.

#### PHASE 5 -- Portable Methodology

Attendees leave with a three-question audit they can run against any agent sandbox they deploy -- including internally built ones.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Pairs directly with Roblox's 'Caging the Agent' (0x0A) and CVE-2026-25725, the real Claude Code sandbox escape where an unprotected settings.json allowed persistent hooks executing with host privileges. Together they make the point that agent sandboxes are young, assumption-laden, and must be validated rather than trusted -- especially in regulated environments where the sandbox is the control you told your auditor about.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Run the three-question audit on every agent sandbox you deploy: what is claimed, what is assumed, can the execution path violate it?

**[2]** Don't treat a vendor sandbox as a compliance control until you've tested the assumption behind its enforcement.

**[3]** Layer containment beneath the sandbox (OS/VM isolation, egress policy) so a design gap in the agent's own sandbox is not the last line of defense.

**[4]** Track and apply agent-sandbox CVEs promptly (e.g. CVE-2026-25725, patched in Claude Code 2.1.2); these move fast and are easy to miss in normal patch cycles.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**GlobeNewswire -- Novee Researchers to Present Four Sessions across Black Hat USA and DEF CON**  
<https://www.globenewswire.com/news-release/2026/07/28/3334295/0/en/Novee-Researchers-to-Present-Four-Sessions-across-Black-Hat-USA-and-DEF-CON-Uncovering-Vulnerabilities-in-Anthropic-OpenAI-and-Google.html>

**OSV -- CVE-2026-25725: Claude Code sandbox escape via persistent configuration injection**  
<https://osv.dev/vulnerability/CVE-2026-25725>

**NVIDIA -- Practical Security Guidance for Sandboxing Agentic Workflows and Managing Execution Risk**  
<https://developer.nvidia.com/blog/category/cybersecurity>

</details>

---

## 0x14 :: One Percent of the Tokens, All of the Strategy: LLM-Assisted Vulnerability Discovery in IoT and Embedded Firmware

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Cyber-Physical Systems & IoT |
| **WHEN** | Aug 5-6, 2026 (40-minute briefing) |
| **SPEAKER** | Ta-Lun Yen — *(independent / TXOne lineage)* |
| **TAGS** | `firmware` `embedded` `token economy` `LLM-as-strategist` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Applies LLM-assisted vulnerability discovery to IoT and embedded firmware -- a domain historically resistant to automation because of stripped binaries, exotic architectures, and absent source.

> ▸ The title is the thesis: use the model for STRATEGY (where to look, what to hypothesize, how to prioritize) rather than brute-force token spend on whole firmware images. One percent of the tokens, all of the strategy.

> ▸ Sits in Black Hat 2026's AI-driven exploitation-of-hardware cluster, where unchanged embedded attack primitives are being accelerated by AI rather than replaced by it.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Why Firmware Resists Naive LLM Use

Embedded images are large, largely uninteresting, and poorly suited to dumping into a context window. Naive approaches burn enormous token budgets on boilerplate and vendor SDK code while missing the small reachable attack surface.

#### PHASE 2 -- Triage and Reduction

The strategic move is aggressive reduction before the model is consulted: isolate the code that actually parses untrusted input (network services, update handlers, protocol parsers) so model attention is spent where bugs live.

#### PHASE 3 -- Model as Strategist, Tools as Executors

The LLM proposes hypotheses and prioritizes targets; deterministic tooling (disassembly, emulation, fuzzing harnesses) does the verification. This mirrors the 'move responsibility toward deterministic code' lesson from the HTTP Terminator work (0x04) -- convergent methodology across two independent teams.

#### PHASE 4 -- Validation Loop (redacted)

Candidate findings are confirmed against emulated or physical targets. Specific vulnerable devices, harness construction, and triggering inputs are withheld here.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 5 -- Economic Consequence

Driving cost down by ~two orders of magnitude changes who can afford firmware bug hunting at scale -- the same economic argument as the fine-tuned OSS model talk (0x07), applied to embedded targets.

### ▚ REAL-WORLD :: WHERE THIS LANDS

IoT and OT fleets are long-lived, rarely patched, and enormous in number. Cheap LLM-guided discovery means the backlog of latent firmware bugs in deployed devices becomes economically worth mining. Utilities, manufacturers, medical device operators, and anyone with a decade-old embedded fleet should assume discovery cost against their devices just fell sharply.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Assume your firmware's latent bugs are now cheap to find; prioritize SBOM coverage and update capability for embedded fleets.

**[2]** Focus hardening on untrusted-input parsers (network services, update handlers, protocol stacks) -- the same surface the strategy targets.

**[3]** Run the same LLM-guided triage defensively against your own images before shipping.

**[4]** Segment OT/IoT networks so a firmware bug does not translate into lateral movement; the discovery economics changed, the network controls still work.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Black Hat USA 2026 -- Session page (One Percent of the Tokens)**  
<https://blackhat.com/us-26/briefings/schedule/#one-percent-of-the-tokens-all-of-the-strategy-llm-assisted-vulnerability-discovery-in-iot-and-embedded-firmware-53075>

**LastPass -- Complete Guide to Black Hat USA 2026 (session listing)**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

**Onit Security -- Black Hat 2026: The Real Theme Is Speed**  
<https://onit.security/blog/black-hat-2026-briefings-forecast/>

</details>

---

## 0x15 :: Catch Me If You Can: AI Investigators Hunting Autonomous Attackers as a Benchmark

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Threat Hunting & Incident Response |
| **WHEN** | Aug 5-6, 2026 (40-minute briefing) |
| **SPEAKER** | Jayson Grace, Martin Wendiggensen; contributor Shane Caldwell — *(security research collaboration)* |
| **TAGS** | `AI defenders` `benchmark` `autonomous attacker` `blue-team evaluation` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Flips the year's dominant offensive framing: instead of building autonomous attackers, build autonomous INVESTIGATORS and measure how well they hunt autonomous attackers.

> ▸ The contribution is a BENCHMARK. Making defensive AI measurable against a live autonomous adversary is the necessary complement to HalCTF's offensive benchmark (0x0E) -- both sides of the arms race now have scoreboards.

> ▸ Directly addresses the blind spot named repeatedly across the conference: when a permitted process makes a permitted request, traditional detection has nothing to fire on. An AI investigator reasons about intent, not signatures.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Detection Gap

Autonomous attacks look like legitimate activity (see Roblox, 0x0A: EDR saw nothing because there was nothing anomalous to see). Signature and anomaly detection both underperform when the attacker uses permitted tools in permitted ways.

#### PHASE 2 -- Investigator Agents

Defensive agents are given telemetry and tasked with reconstructing what happened -- correlating across sources and reasoning about whether a sequence of individually benign actions constitutes an attack.

#### PHASE 3 -- Adversary as Benchmark Generator

Rather than fixed test cases, an autonomous attacker generates the scenarios. This yields adaptive, non-memorizable evaluation -- the defensive analogue of class-agnostic testing.

#### PHASE 4 -- Scoring

Investigator performance is measured (detection, attribution, reconstruction quality), turning 'our AI helps the SOC' marketing claims into a comparable metric.

#### PHASE 5 -- Feedback

Benchmark results identify where AI investigators systematically fail, feeding back into both tooling and analyst workflow design.

### ▚ REAL-WORLD :: WHERE THIS LANDS

For a SOC evaluating AI-assisted triage vendors, a benchmark against autonomous attackers is exactly the missing procurement artifact. It also connects to the AI Village poster work on human rubber-stamping in agent oversight: if reviewers approve without verifying, and investigators are unmeasured, the whole defensive loop is unvalidated.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Demand measured evidence from AI-defense vendors; a benchmark against adaptive autonomous attackers beats a demo against replayed IOCs.

**[2]** Build detection around intent and sequence reconstruction, not just anomalous artifacts -- permitted-process/permitted-request attacks defeat the latter.

**[3]** Instrument agent activity as a first-class telemetry source so investigators have something to reason over.

**[4]** Measure your human oversight too: unverified approvals nullify the value of good investigator output.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Black Hat USA 2026 -- Session page (Catch Me If You Can)**  
<https://blackhat.com/us-26/briefings/schedule/#catch-me-if-you-can-ai-investigators-hunting-autonomous-attackers-as-a-benchmark-53869>

**Onit Security -- Black Hat 2026: The Real Theme Is Speed**  
<https://onit.security/blog/black-hat-2026-briefings-forecast/>

**LastPass -- Complete Guide to Black Hat USA 2026 (session listing)**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

</details>

---

## 0x16 :: Rules for Neural Traffic: A New Defensive Layer for LLMs

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | Defense & Resilience // AI, ML & Data Science |
| **WHEN** | Aug 5-6, 2026 (40-minute briefing) |
| **SPEAKER** | Yisroel Mirsky & Shir Rozenfeld; contributors Gilad Gressel, Rahul Pankajakshan — *Ben-Gurion University (Offensive AI Research Lab lineage)* |
| **TAGS** | `defensive layer` `IDS-for-LLM` `neural traffic` `detection rules` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Proposes a NEW defensive layer for LLMs -- treating the model's internal/neural traffic as an inspectable channel with rules, analogous to how network IDS inspects packets rather than trusting endpoints.

> ▸ Strategically important because it targets the layer everything else at this conference proved insufficient: prompt-level and response-level filtering. A defense operating on neural traffic sees things a text filter cannot.

> ▸ One of the few genuinely DEFENSIVE architecture contributions in the 2026 AI track, from an academic group with a strong offensive-AI research pedigree.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Why Text-Level Guardrails Fail

Prompt filters and output filters inspect the surface. Attacks repeatedly evade them by hiding intent in encoding, structure, or context (see AI browsers, 0x10, where tag mimicry and URL-fragment exfil bypassed layered scanning).

#### PHASE 2 -- Neural Traffic as an Observable

The proposal treats signals inside the model's processing as an inspectable stream, giving defenders a vantage point closer to what the model is actually doing than to what it was asked.

#### PHASE 3 -- Rule Construction

Rules are defined over that stream -- the IDS analogy is explicit: signatures and behavioral rules applied to neural traffic rather than to text.

#### PHASE 4 -- Detection & Response

Matching rules flag or block, providing a control point independent of the prompt channel and therefore not bypassable by the same evasions.

#### PHASE 5 -- Position in the Stack

Presented as an additional LAYER, not a replacement -- consistent with the conference-wide conclusion that no single control suffices and defense-in-depth is the only viable posture.

### ▚ REAL-WORLD :: WHERE THIS LANDS

For enterprises self-hosting or fine-tuning models, a neural-traffic inspection layer is deployable in a way that vendor-side guardrails are not. It's most relevant where you control the inference stack -- which is increasingly common as orgs run private models for data-sovereignty reasons (and, per 0x07, as attackers do the same).

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Add a detection layer that does not depend on the prompt channel; controls sharing a bypass path with the attack are not independent controls.

**[2]** Where you control inference, instrument it -- self-hosting gives defensive visibility that API consumption does not.

**[3]** Combine with execution-layer governance (0x03, 0x08): inspect what the model does as well as how it reasons.

**[4]** Treat this as an emerging research direction; validate claimed detection rates in your own environment before relying on it as a primary control.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Black Hat USA 2026 -- Session page (Rules for Neural Traffic)**  
<https://blackhat.com/us-26/briefings/schedule/#rules-for-neural-traffic-a-new-defensive-layer-for-llms-53675>

**LastPass -- Complete Guide to Black Hat USA 2026 (session listing)**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

</details>

---

## 0x17 :: The AI-Assisted Discovery Cluster: 0-Day Engine / Prompt2Own / Beyond Detection / Closed Loop

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Offensive + Defense |
| **WHEN** | Aug 5-6, 2026 |
| **SPEAKER** | Multiple presenting teams — *(various)* |
| **TAGS** | `LLM vuln discovery` `kernel exploitation` `triage` `exploit-to-defense loop` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Four sessions form a single arc -- AI compressing the entire vulnerability lifecycle. THE 0-DAY ENGINE: authors report using LLMs to find 100+ vulnerabilities in Chrome and Android. PROMPT2OWN: kernel exploit development with a model in the loop.

> ▸ On the defensive side, BEYOND DETECTION tests AI approaches to separating real vulnerabilities from noise, and CLOSED LOOP runs the full cycle -- working exploit to deployed defense -- in a promised five minutes.

> ▸ The economic thesis, stated plainly by conference observers: the expensive part of hacking has always been the front end -- finding a flaw and proving it's real. That is precisely the part AI is now compressing.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Discovery at Scale (The 0-Day Engine)

LLM-driven discovery applied to two of the most heavily audited codebases on earth (Chrome, Android) yielding 100+ vulnerabilities. The significance is not any single bug but that saturated targets still yield at volume under AI-assisted review.

#### PHASE 2 -- Weaponization Assistance (Prompt2Own) (redacted)

Kernel exploit development with a model in the loop -- historically the most expert-gated step in offensive security. Technique detail is fully withheld; only the existence and direction of the capability is reported here.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Triage (Beyond Detection)

Defensive counterpart: when discovery becomes cheap, the bottleneck moves to distinguishing real, reachable vulnerabilities from noise. This session evaluates AI approaches to that filtering problem.

#### PHASE 4 -- Remediation (Closed Loop)

Completes the cycle: from a working exploit to a deployed defense in a claimed five minutes. If discovery compresses for attackers, response must compress for defenders or the gap widens permanently.

#### PHASE 5 -- The Combined Picture

Read together, the cluster describes a lifecycle where each stage -- find, weaponize, triage, fix -- is being automated in parallel. The strategic question for defenders is which stage compresses FASTEST, since the differential determines who benefits.

### ▚ REAL-WORLD :: WHERE THIS LANDS

For any organization shipping software, the practical implication is that time-to-exploit for newly disclosed bugs is shrinking while the volume of discovered bugs rises. Patch cadence, exposure windows, and vulnerability-management SLAs designed for a slower era are the control most likely to break first -- and 'we're a hard target, we've been audited' is no longer protective when Chrome and Android still yield at volume.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Compress your own response loop; if attacker discovery accelerates and your patch cycle doesn't, the exposure window grows regardless of your control quality.

**[2]** Invest in reachability-aware triage so rising discovery volume doesn't drown your team in unexploitable findings.

**[3]** Adopt AI-assisted discovery internally -- the asymmetry favors whoever finds the bug first, and that is a choice you control.

**[4]** Re-baseline vulnerability-management SLAs against an assumption of faster exploit availability, especially for internet-facing and kernel-adjacent surfaces.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Onit Security -- Black Hat 2026: The Real Theme Is Speed**  
<https://onit.security/blog/black-hat-2026-briefings-forecast/>

**Black Hat USA 2026 -- Briefings Schedule (official)**  
<https://blackhat.com/us-26/briefings/schedule/index.html>

**LastPass -- Complete Guide to Black Hat USA 2026**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

</details>

---

## VOLUME III :: KINETIC, ECOSYSTEM &amp; THE HUMAN LAYER

> Volume III leaves the screen. It covers prompt injection delivered through a robot dog's own camera and microphone, the AI notetaker sitting silently inside government and corporate calls, the identity boundaries that stop meaning anything when an agent acts as you, the offense-defense policy debate with its 1995 historical control, and the defensive counterweight of autonomous adversary emulation.

---

## 0x18 :: Kinetic Prompt Injection: Jailbreaking a Robot Dog Through Its Own Eyes and Ears

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 |
| **TRACK** | AI, ML & Data Science // Cyber-Physical Systems |
| **WHEN** | Aug 6, 2026 10:15 AM (Oceanside C) |
| **SPEAKER** | Research team, BT6 — *BT6* |
| **TAGS** | `embodied AI` `Unitree Go2` `Gemini Robotics-ER 1.6` `sensor-channel injection` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ The abstract describes a LIVE jailbreak of a stock Unitree Go2 robot dog running Gemini Robotics-ER 1.6 -- reached through its own camera and microphone, and driven to physical movement, with NO human in the loop.

> ▸ This is the moment prompt injection stops being a text problem. The attack channel is the robot's own perception: it was talked into moving by something it SAW and something it HEARD.

> ▸ The Go2 is commercially available from roughly $1,600-$2,200 and has been deployed for property security, disaster relief, and on battlefields -- so the target platform is neither exotic nor hypothetical.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Embodied Agents Collapse the Air Gap

A vision-language-action model turns perception directly into actuation. There is no keyboard, no chat box, and no network foothold required: whatever the sensors ingest becomes potential instruction. The 'input validation' boundary is now physical space.

#### PHASE 2 -- The Sensor as Injection Channel (redacted)

Attacker-controlled content is placed where the robot's camera and microphone will perceive it during normal operation. The specific presentation, framing, and audio construction that achieve reliable injection are withheld entirely -- this is the sharpest end of the whole dossier, because the output is physical motion.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 3 -- Perception-to-Action Translation

The robotics model interprets perceived content as task instruction rather than as environmental data. This is exactly the same trust collapse documented in AI browsers (0x10) and agent frameworks (0x06) -- untrusted input inheriting the agent's authority -- but the authority here is a 15kg machine that can move at 3.7 m/s.

#### PHASE 4 -- Autonomous Physical Execution

The robot is driven to movement with no human in the loop. The absence of a confirmation step is the critical design property: in software, human-in-the-loop is a mitigation; in robotics, latency requirements often preclude it.

#### PHASE 5 -- Why This Reframes the Threat Model

Every prior entry in this dossier ends in data loss, credential theft, or unauthorized transactions. This one ends in kinetic effect. Safety engineering and security engineering stop being separable disciplines at this point.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Quadrupeds and similar embodied platforms are already deployed for perimeter patrol, industrial inspection, disaster response, and military use. A perception-channel injection against a security patrol robot could redirect it, blind it, or induce unsafe motion near people. Because the attack arrives through the sensors, network segmentation, EDR, and API authentication -- the entire conventional control stack -- provide no coverage whatsoever.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Treat all sensor input as untrusted instruction-bearing data; perception is now an attack surface requiring validation, not a trusted feed.

**[2]** Architecturally separate PERCEPTION from COMMAND: environmental observation should inform a planner, never directly author privileged actions.

**[3]** Enforce hard physical safety envelopes outside the model -- speed, geofence, and proximity limits implemented in deterministic control logic the model cannot override.

**[4]** Require out-of-band authorization for high-consequence physical actions, accepting the latency cost where human safety is at stake.

**[5]** Assume vendor guardrails are insufficient (see 0x10: every layered defense tested was bypassed) and add independent, non-ML interlocks.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**UNAPOLOGETICALLY DAHLING -- Why Is the Scariest Morning at Black Hat 2026 a Thursday at 10:15?**  
<https://unapologeticallydahling.com/blog/black-hat-2026-the-most-terrifying-morning-in-vegas>

**Black Hat USA 2026 -- Briefings Schedule (official)**  
<https://blackhat.com/us-26/briefings/schedule/index.html>

**TIME -- Unitree Robotics (Go2 platform, pricing and deployment context)**  
<https://www.aol.com/unitree-robotics-112824308.html>

</details>

---

## 0x19 :: The Silent Participant: AI Notetaker Exposure Across Government and Corporate Video Calls

| | |
| :--- | :--- |
| **VENUE** | Black Hat USA 2026 week -- disclosure (NOT a briefing) |
| **TRACK** | Conference-week research disclosure // AppSec, Cloud |
| **WHEN** | Disclosed Aug 4, 2026 (research conducted from late January 2026) |
| **SPEAKER** | BobDaHacker (independent researcher); reported by Nate Nelson — *independent / Dark Reading* |
| **TAGS** | `tl;dv` `Firebase/Firestore misconfiguration` `tenant isolation` `notetaker OAuth sprawl` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ SCOPE NOTE: this is conference-week disclosure, not an accepted Black Hat or DEF CON talk. It is included because it is the clearest real-world illustration of the 'silent participant' agent-identity problem the con spent three days theorizing.

> ▸ A missing Firestore isolation rule on ONE collection in tl;dv -- an AI meeting assistant claiming 2M+ users -- let any authenticated user query every live conference call in the world into which tl;dv had been invited, plus meeting metadata and creator email addresses.

> ▸ Exposure found: 180,000+ completed call records across 80,000+ users, spanning governments of 23 countries, HubSpot, Mitsui Fudosan, UC Berkeley, and the University of Tokyo. The researcher joined live calls roughly 80% of the time by impersonating a notetaker bot and requesting entry.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Trust Position of a Notetaker

Notetakers join, record, and transcribe by default; they require video, audio, and usually calendar and contact access. As the researcher puts it, they are a silent participant with deep access to the communication layer -- and most people treat them like a browser extension they installed and forgot.

#### PHASE 2 -- The Single Missing Rule

Tenant isolation was correctly applied to transcripts, recordings, and chats. It was absent on the 'meetings' collection alone. One unscoped container was enough to expose the global meeting graph -- a reminder that isolation is only as good as its least-covered object.

#### PHASE 3 -- Metadata to Access (redacted)

Meeting information alone does not grant entry. The researcher found that impersonating a notetaker bot and requesting to join typically succeeded. The operational specifics are withheld; the defensive lesson is that a bot join request is socially unremarkable and almost never challenged.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Secondary Leakage

Of ~27,000 sampled meeting IDs, over 1,000 exposed invitee emails and transcripts on the open internet -- including a Ukrainian Ministry of Digital Transformation meeting and a Sao Paulo state government session. Notably, ~69,000 of 70,000 meetings were protected by privacy settings ALONE, which is the one control that actually held.

#### PHASE 5 -- The Disclosure Failure

The researcher could not get the vendor to respond; press outreach also went unanswered, and the issue remained live at publication. The governance gap is as instructive as the technical one.

### ▚ REAL-WORLD :: WHERE THIS LANDS

This is the most immediately actionable item in the dossier for a security program. Notetakers sit inside privileged conversations by default, carry broad OAuth scopes, and receive almost no procurement scrutiny. In one documented case a bot sat in a Malaysian government training meeting where 157 participants saw it in the roster and nobody questioned it. Legal, board, M&A, and IR calls are the obvious high-value exposures.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Treat the bot as a participant: if an AI notetaker appears in a call you did not invite, that is a red flag worth stopping the meeting over.

**[2]** Default meetings to private. Privacy settings were the control that actually protected ~69,000 of 70,000 meetings in this dataset.

**[3]** Inventory notetaker OAuth grants across your tenant and scope them down; these tools routinely hold calendar, contact, video, and audio access nobody reviewed.

**[4]** For vendors: scope Firestore reads to the authenticated user's organization -- the fix here is a few lines of security rules, and Google's default rules warn you.

**[5]** Establish a policy for which meeting classifications may admit AI notetakers at all, and enforce it in the meeting platform rather than by convention.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**Dark Reading -- AI Notetaker Lets Hackers Spy on Government, Corporate Video Calls**  
<https://www.darkreading.com/application-security/ai-notetaker-spy-government-corporate-video-calls>

**BobDaHacker -- tl;dv research write-up**  
<https://bobdahacker.com/blog/tldv-hack>

**Brinztech -- AI Meeting Assistant Vulnerabilities Expose Corporate and Government Video Calls**  
<https://www.brinztech.com/breach-alerts/brinztech-alert-ai-meeting-assistant-vulnerabilities-expose-corporate-and-government-video-calls>

</details>

---

## 0x1A :: That's Not Your Agent: Why Zero Trust Can't Tell (+ the Identity Boundary Cluster)

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 |
| **TRACK** | Creator Stage 1 & 2 // Identity, Trust, Influence |
| **WHEN** | Aug 8, 2026 (2:30 PM, 4:30 PM, 5:30 PM slots) |
| **SPEAKER** | Krity Kharbanda & Emma Yuan Fang; Tobias Diehl; Julie Brunias — *(various)* |
| **TAGS** | `agent identity` `zero trust` `trust amplification` `influence operations` `SADF taxonomy` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Three Saturday DEF CON sessions converge on one problem: the identity boundaries that quietly stop meaning anything once an agent is acting on your behalf. Zero Trust authenticates principals -- but an agent acting AS you presents as you.

> ▸ TRUST AMPLIFICATION (Tobias Diehl) documents Microsoft Copilot case studies where enterprise AI systems enable AI-ASSISTED INFLUENCE OPERATIONS: the assistant's institutional credibility is borrowed to make manipulated content persuasive.

> ▸ SADF (Julie Brunias) contributes a taxonomy and evaluation framework for agentic security failures -- the field acquiring shared vocabulary, which is what a discipline does when it stops being a novelty.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Delegation Problem

When an agent acts on a user's behalf it carries that user's identity and entitlements. Zero Trust's core question -- 'is this principal who they claim?' -- returns TRUE even when the agent has been hijacked, because the credential is legitimately the user's.

#### PHASE 2 -- Trust Amplification

An enterprise assistant carries institutional authority. Content surfaced through it inherits credibility the same content would not have in an email. This turns a compromised or steered assistant into an influence vector rather than merely a data-loss vector.

#### PHASE 3 -- Influence Operations Inside the Enterprise (redacted)

Case studies demonstrate driving an enterprise assistant to shape what employees believe and decide. Specific manipulation techniques are withheld; the concept matters more than the recipe -- this is an integrity attack, not a confidentiality attack, and most controls are built for the latter.

```text
████████████████████████████████████████████████████████████████████████████
██                                                                        ██
██   ▓▒░  R E D A C T E D  ::  WEAPONIZABLE DETAIL WITHHELD  ░▒▓          ██
██                                                                        ██
██   ████████████████████  ██████████████  ████████████████████████████   ██
██   ██████████  ████████████████████████████████  ██████████            ██
██   ████████████████████████  ██████████  ████████████████████████████  ██
██                                                                        ██
██   [ operational payload / exploit steps removed for research-only      ██
██     distribution -- analysis, threat model and defenses retained ]     ██
██                                                                        ██
████████████████████████████████████████████████████████████████████████████
```

#### PHASE 4 -- Naming the Failures (SADF)

A taxonomy and evaluation framework lets teams classify and compare agentic security failures instead of treating each incident as sui generis. Pairs with the benchmarking work in 0x0E and 0x15.

#### PHASE 5 -- What Zero Trust Needs Next

The cluster's implication: identity systems need to distinguish 'the user' from 'an agent acting for the user,' carry delegation context and purpose, and support revocation of agent authority independent of user authority.

### ▚ REAL-WORLD :: WHERE THIS LANDS

Directly relevant to any enterprise with an SSO-integrated assistant. Your IdP logs show the user; your DLP sees an authorized principal; your audit trail is technically accurate and substantively misleading. The influence-operations angle is especially underrated in regulated industries, where an assistant shaping employee decisions is a control failure with compliance consequences, not just a security one.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Model agent identity as distinct from user identity; issue agents their own credentials with delegation context rather than letting them wear the user's.

**[2]** Support independent revocation: you must be able to kill an agent's authority without disabling the human.

**[3]** Extend monitoring to integrity, not just confidentiality -- track what the assistant TELLS people, not only what data it touches.

**[4]** Adopt a shared failure taxonomy (e.g. SADF) so incidents are comparable across teams and over time.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**AI Village @ DEF CON 34 -- Schedule (Saturday DEF CON stage sessions)**  
<https://aivillage.org/events/defcon-34/>

**DEF CON 34 -- Creator Stage Talks (official)**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**AI Village -- Poster archive (identity & governance posters)**  
<https://aivillage.org/posters/>

</details>

---

## 0x1B :: Minimize Harm, Maximize Defense: How Anthropic Navigates the Offense-Defense Divide (+ the SATAN Retrospective)

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 |
| **TRACK** | Creator Stage 4 & 2 // Policy, Product Safety, History |
| **WHEN** | Aug 8, 2026 12:00-12:45 PM (Barnard); 2:00-2:30 PM (Crume) |
| **SPEAKER** | Curt Barnard (Anthropic); Jeff Crume — *Anthropic; IBM (Crume)* |
| **TAGS** | `dual-use` `safeguards` `disclosure history` `SATAN` `Mythos` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ Anthropic's Curt Barnard addresses the product-safety side of the year's central argument: how a frontier lab decides what capability to ship when the same capability serves attackers and defenders.

> ▸ Jeff Crume's 'What we learned from SATAN about the MYTH of Mythos' supplies the historical control. SATAN (1995) provoked identical panic -- a tool that automated finding others' weaknesses, released publicly, allegedly arming attackers.

> ▸ Together with the Friday keynote panel (0x0D), these form the conference's policy spine: three vantage points -- history, product safety, and defense at scale -- on whether restricting dual-use capability protects defenders or hands attackers the advantage.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- The Structural Bind

Vulnerability discovery, exploit reasoning, and autonomous operation are the SAME capabilities whether the operator is red or blue. There is no clean technical separation to engineer around.

#### PHASE 2 -- Safeguards and Their Costs

Conservative safeguards catch benign use; permissive ones enable misuse. The honest framing is that this is a calibration problem with real error rates on both sides, not a solvable one.

#### PHASE 3 -- The SATAN Precedent

In 1995, SATAN's release was widely predicted to arm attackers en masse. The retrospective asks what actually happened, and what that says about the current round of predictions regarding frontier models.

#### PHASE 4 -- The Counter-Evidence in the Room

The rest of this dossier complicates any comfortable conclusion: NVIDIA's talk (0x07) shows a 30B open model matching frontier offensive performance at 70-125x less cost. Restriction at the frontier does not restrain a fine-tuned OSS model running privately on someone's own hardware.

#### PHASE 5 -- Practical Posture

For practitioners the actionable synthesis is: assume adversary access to capable AI regardless of vendor policy, and invest accordingly in containment, detection, and response rather than in hoping capability stays scarce.

### ▚ REAL-WORLD :: WHERE THIS LANDS

This determines what tooling your team can legitimately buy and build. If you are standing up an AI red-team function, the policy trajectory discussed here shapes vendor availability, contractual constraints, and eventually regulatory exposure. It is also the frame for explaining to executives why you cannot simply prohibit the technology into safety.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Write an explicit organizational dual-use policy for AI capability instead of deciding case-by-case under pressure.

**[2]** Plan on the assumption that adversaries have capable, private, cheap models; do not treat vendor restrictions as a defensive control.

**[3]** Participate in disclosure and governance norms -- outcomes here are shaped by community practice, not by any single vendor's policy.

**[4]** Use the historical record (SATAN and successors) to calibrate predictions rather than reasoning from first principles about an unprecedented technology.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**AI Village @ DEF CON 34 -- Schedule (Saturday DEF CON stage sessions)**  
<https://aivillage.org/events/defcon-34/>

**DEF CON 34 -- Creator Stage Talks (official)**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**Dark Reading -- Anthropic: Claude Attacks Result of Security Gaps, Not Model Issues**  
<https://www.darkreading.com/cyber-risk>

</details>

---

## 0x1C :: Scaling Adversary Emulation with Autonomous Agents (+ AgentBreaker & MeshLens)

| | |
| :--- | :--- |
| **VENUE** | DEF CON 34 |
| **TRACK** | Creator Stage 1 / Community Stage / AI Village |
| **WHEN** | Aug 7, 2026 4:00 PM & 4:30 PM; Aug 8, 4:00-5:00 PM |
| **SPEAKER** | Daniel Fabian (Google); Aditi Narasimhan & Farzaan Kaiyom; Vipul Ujawane, Jigar Bhavsar & Rayden Chia (Google) — *Google; independent* |
| **TAGS** | `autonomous red team` `adversary emulation` `coding-agent blind spots` `security profiling` |

### ▚ BLUF :: BOTTOM LINE UP FRONT

> ▸ The defensive counterweight to the offensive agent research: Google's Daniel Fabian on scaling ADVERSARY EMULATION with autonomous agents -- using the same capability that worries everyone, pointed inward.

> ▸ AGENTBREAKER (Narasimhan & Kaiyom) is a blind-spot detector for coding agents -- tooling aimed squarely at the failure mode behind the Roblox incident (0x0A) and the Novee harness findings (0x11-0x13).

> ▸ MESHLENS (Google) covers security profiling at scale, completing a picture where defenders industrialize agent-driven testing rather than conceding the automation advantage to attackers.

### ▚ THE BREAKDOWN :: LOGICAL PHASES

#### PHASE 1 -- Emulation as the Defensive Use Case

Adversary emulation is the least ambiguous defensive application of offensive AI: you attack yourself, continuously, at machine speed, in an environment you own.

#### PHASE 2 -- Scaling Beyond Human Red Teams

Human red teams are expensive and periodic; autonomous emulation is continuous. The stated industry problem is that attackers compress timelines dramatically -- the window between vulnerability and exploitation can shrink to minutes, which periodic assessment cannot cover.

#### PHASE 3 -- Finding Coding-Agent Blind Spots (AgentBreaker)

Purpose-built detection for where coding agents fail, addressing the exact class documented repeatedly across both conferences: agents doing permitted things for unauthorized reasons.

#### PHASE 4 -- Profiling at Scale (MeshLens)

Security profiling across a large estate, so results from autonomous emulation translate into prioritized, actionable posture rather than an undifferentiated finding dump.

#### PHASE 5 -- Closing the Asymmetry

Read against 0x07 (cheap offensive models) and 0x17 (compressed discovery), this cluster is the defender's answer: if discovery is automating, defensive discovery must automate at the same rate or the exposure window grows permanently.

### ▚ REAL-WORLD :: WHERE THIS LANDS

This is the build-vs-buy roadmap for an AI-era security program. For a red team lead, the practical question is which parts of your engagement lifecycle can be handed to autonomous emulation (broad coverage, regression, continuous validation) and which still require human creativity (novel chains, business-logic abuse, social engineering). The cluster suggests the boundary is moving.

### ▚ DEFENSE :: HOLD THE LINE

**[1]** Stand up continuous autonomous adversary emulation; periodic assessment cannot match an adversary operating at machine speed.

**[2]** Deploy coding-agent blind-spot detection specifically -- generic AppSec tooling does not model agent authority abuse.

**[3]** Pair automated discovery with scaled profiling so output becomes prioritized posture rather than noise.

**[4]** Keep humans on novel-chain and business-logic work where autonomous agents remain weakest, and let automation own breadth and regression.

<details>
<summary><b>&#9656; sources for this entry</b></summary>

**AI Village @ DEF CON 34 -- Schedule (Friday & Saturday sessions)**  
<https://aivillage.org/events/defcon-34/>

**Dark Reading -- AI Harnesses Burst With Potential Exploit Opportunities**  
<https://www.darkreading.com/application-security/ai-harnesses-potential-exploit-opps>

**DEF CON 34 -- Creator Stage Talks (official)**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

</details>

---

## 0x1D :: APPENDIX A :: The Full Poster Roster (DC34 AI Village)

AI Village accepted **34 poster presentations** at DEF CON 34, themed on *adversarial attacks against agents and agentic systems* — the first poster track the village has run. Two or three ran in each hour-long block Friday and Saturday in LVCC W603, with authors present to defend them. The complete roster is catalogued below, grouped thematically rather than by time slot, with a one-line analytic note on each and cross-references to the main entries. Titles and authors are as listed by AI Village; a few appear under slightly different titles in the schedule versus the archive, and both variants are preserved where they differ.

> The village's own summary of what the roster shows is worth repeating: prompt injection arrives through telemetry, phone calls, Slack, and product descriptions; malicious context spreads between MCP servers and from one agent to the next; privilege boundaries give way inside CI/CD and agentic commerce. Much of the rest is about catching it.

### ▚ GROUP A :: INJECTION THROUGH UNEXPECTED CHANNELS

*Prompt injection no longer arrives by prompt. It arrives through telemetry, phone calls, Slack, product descriptions, and the extensibility surfaces of coding tools.*

| Poster | Authors | Note |
| :--- | :--- | :--- |
| **Poisoning the SOC: Prompt Injection via Ingested Telemetry** | John Seymour (Salesforce) | Injection delivered through the logs the SOC's own AI ingests -- the defender's data pipeline as attack path. |
| **For Prompt Injection, Press 1: Hacking AI Voice Agents** | Willie Zhang (ProCircular) | The telephone as an injection channel; voice agents inherit the whole class. |
| **Confused Deputies in Slack: Exploiting Agentic AI in Production Environments** | Rodney Beede (Life360) | Classic confused-deputy, agentic edition, in a live production chat platform. |
| **Poisoned Mandates: Stealing Agency from Agentic Commerce, One Product Description at a Time** | Aaryan Bhujang, Saish Bhorpe, Aryaman Behera (Repello AI) | A single crafted product description hijacks a shopping agent's mandate -- pairs with the retailer compromise in 0x08. |
| **MCP (Malicious Context Propagation): Weaponizing the Extensibility of AI Coding Assistants** | Roshan Piyush, Soujanya Namburi (Harness) | Extensibility as attack surface: the plugin model becomes the delivery model. |
| **From Recon to Full System Prompt Exfiltration: A 5-Stage Attack Chain Against a Production LLM Chatbot** | Veli Oguzcan Akdag (Bilisim Cyber Security & AI) | A complete documented chain against a production chatbot, recon through exfil. |

### ▚ GROUP B :: PROPAGATION, WORMS & CROSS-AGENT BOUNDARIES

*Once agents talk to agents, compromise stops being local. This group documents the worm dynamics and privilege-boundary failures of connected agent ecosystems.*

| Poster | Authors | Note |
| :--- | :--- | :--- |
| **MCParasite: Tool Poisoning and Agent-to-Agent Worm Propagation in MCP-Based AI Systems** | Utku Yildirim (Cobalt.io & Hoffmann Cybersecurity), Ozgun Kultekin (Trendyol Group) | The canonical agent-worm paper of the cycle; underpins the fireside chat in 0x0C. |
| **I'll Just Call You -- Agent-to-Agent Privilege Boundary Failures in CI/CD Agents** | Dan Lisichkin (Pillar Security) | Privilege boundaries dissolving between chained CI/CD agents -- the poster companion to 0x11. |
| **Reference Grafting in A2A: Cross-Principal Task-Data Exfiltration via referenceTaskIds** | Shay Sakazi, Sunders Bruskin, Emil Gelman (AI Village) | Protocol-level exfiltration across principals in the A2A spec -- a standards bug, not an implementation bug. |
| **AI Agents Escape Their Task Horizon** | Emile Delcourt (OWASP ASI) | Agents exceeding the scope of the task they were given -- scope creep as a security property. |
| **Your AI Agent's Backend Is a Crime Scene: The Supply Chain Problem Haunting Every Organization** | Eli Woodward | The infrastructure beneath the agent, echoing the Ray botnet findings in 0x05. |
| **The Ouroboros Loop: Breaking Interactive LLM Workspace Sandboxes** | Mehmet Onder Key | Workspace sandbox escapes -- the poster-track counterpart to 0x09 and 0x13. |

### ▚ GROUP C :: GUARDRAIL & MEMORY FAILURES

*Where the defenses themselves become the vulnerability, and where agent memory turns into a persistence mechanism.*

| Poster | Authors | Note |
| :--- | :--- | :--- |
| **Block Means Yes: Extracting Protected Agent Data Through a Guard LLM's Own Refusal Signal** | Larry Suto | The guard model's refusal becomes a side channel -- the defense leaks what it protects. |
| **Poison In, Poison Out: CDC-Aware Containment for RAG and Agent Memory** | Kunal Jain | Containment strategy for poisoned RAG and memory stores; defensive counterpart to the memory poisoning in 0x06. |
| **Memory Laundering, Pressure Points, and Other Agent Failure Modes** | Vincent Abruzzo, Greg Kocher, Neel Nanda, Arthur Conmy | Taxonomy of memory-layer failure modes, including laundering poisoned context into trusted state. |
| **ARM: Agent Reasoning Markup -- Detecting Sycophantic Drift and Silent Position Reversals in Multi-Agent AI** | Erik Roed | Detecting agents quietly reversing position under pressure -- an integrity failure with no obvious artifact. |
| **The Agentic Free Pass: Does an Abliterated Backbone Make Agents Easier to Attack?** | Karol Piekarski, Nishith Sinha | Whether stripping safety training from the backbone materially weakens the agent built on it. |
| **Don't Block -- Bifurcate** | Kastriot Fetahaj (Kosova Cyber Team), Robert Shala (DefCon Group Prishtina), Blerim Rexha (University of Prishtina) | An architectural alternative to blocking as the primary guardrail response. |

### ▚ GROUP D :: DETECTION, RUNTIME DEFENSE & THE SOC

*The largest defensive cluster: catching agent compromise at runtime, and making the SOC work when the attacker is autonomous.*

| Poster | Authors | Note |
| :--- | :--- | :--- |
| **Attackers Don't Need Shells, They Need Prompts: This Is How We Hunt Them** | Raz Tel-Vered (Zenity) | Hunting methodology for a world where the payload is language, not a binary. |
| **Detecting Unauthorized Tool Calls Using Ollama and Splunk** | Anshumaan Mishra (Independent) | Practical, deployable detection for the exact primitive abused in 0x03. |
| **The Model Is the Malware: Runtime Behavioral Detection of Malicious ML Artifacts** | Hala Ali (Virginia Commonwealth University), Andrew Case (Volexity) | Treating the model artifact itself as the malicious object, caught by behavior at runtime. |
| **The Weight of Evidence: How an Agentic SOC Analyst Earns Your Trust** | Sophena Wilson (Microsoft) | What an autonomous SOC analyst must show to be trusted -- the trust-calibration problem from the defender's side. |
| **Engineering Autonomous Security Agents for Defense at Scale** | Dominik Swierad, Olga Shulman (Google) | Production engineering for defensive agents at Google scale. |
| **Silence, with Receipts.** | Matthew Nardizzi (author), James Derella (presenter) (Vortex Black) | Evidentiary approaches to agent activity -- provable accounts of what an agent did. |

### ▚ GROUP E :: RED TEAMING, TOOLING & THE SKILL BARRIER

*Industrializing offensive testing of agents -- and what happens to the skill barrier when intent alone is nearly sufficient.*

| Poster | Authors | Note |
| :--- | :--- | :--- |
| **MiDojo: Red-Team Any Agent in Any Environment** | Sai Chandra Pandraju, Diego Maniloff, Muneeza Azmat, Stuart Battersby, Henrique Nunes, Alessandro Beltramo (Red Hat) | General-purpose agent red-teaming harness. |
| **Policy-Driven Agentic Red Teaming: Automated Indirect Prompt Injection Testing from Risk Assessments** | Muneeza Azmat, Sai Chandra Pandraju, Diego Maniloff, Stuart Battersby, Henrique Nunes, Alessandro Beltramo (Red Hat) | Driving injection testing directly from your risk assessment -- governance to test-case automation. |
| **Prompt Injection Testing at Scale** | Gabriele Randi, Viviana Sutedjo (Google) | Industrialized injection testing across a large product surface. |
| **Beyond CTFs: Engineering AI Agents for Real-World Web Pentesting** | Dhruva Goyal, Sitaraman Subramanian (BugBase) | Moving agent pentesting from CTF conditions to messy production reality. |
| **The Collapse of the Skill Barrier: Building Autonomous CTF Tools Through Pure Intent** | David Kuznicki (Puzzled Hackers) | The accessibility argument stated bluntly -- capability from intent alone. |
| **The Agents of Chaos: AI-Driven Malware Generation** | Arad Donenfeld (SafeBreach) | AI-generated malware, matching the Oligo assessment of AI-authored payloads in 0x05. |
| **Improving AI Red-Teaming by Systematizing Red-Teaming Reports** | Jessica Ji, Colin Shea-Blymyer (CSET) | Making red-team findings comparable and cumulative rather than one-off. |
| **Compiling Expertise: Turning Tribal Knowledge into Auditable Agents** | Nathan Whitaker | Encoding institutional security knowledge into agents that can be audited. |

### ▚ GROUP F :: GOVERNANCE, IDENTITY, OVERSIGHT & GEOPOLITICS

*The human and institutional layer: who approves what, which identity acts, and what nation-state activity looks like in the model supply chain.*

| Poster | Authors | Note |
| :--- | :--- | :--- |
| **Stop Pressing 1: Measuring Human Rubber-Stamping in Agent Oversight** | Rita Sabri | The most quietly damning result in the track: human-in-the-loop fails when the human does not actually verify. |
| **Stop Pressing 1: Do Students Verify Before They Approve? A Pilot Study of Comprehension Gates in Human Oversight of AI Agents** | Rita Sabri (DCPS) | Companion pilot testing comprehension gates as a fix for rubber-stamping. |
| **Securing Cross-Enterprise AI Agents: An Open Source Identity and Governance Case Study** | Sri Aradhyula (Cisco), Sarah Evans (Dell), Shankar Garikapati (Lyft), Amritha Lal (AWS), Manish Singh (Datum) | Multi-vendor identity and governance work -- the constructive answer to 0x1A. |
| **Google's AI Vulnerability Reward Program (AI VRP) / Hacking AI: Real-World Lessons from an AI VRP** | John Kotheimer, Daniel Di Bartolo (Google) | What a year of real AI bug bounty submissions actually looks like. |
| **The Anatomy of a Chinese Knowledge Distillation Campaign** | Colin Shea-Blymyer, Kyle Miller (CSET) | Model capability extraction as a geopolitical activity -- the supply chain above the code. |

### ▚ COMPETITIONS, DEMOS &amp; FIRESIDE CHATS

- **HalCTF: Hostile Autonomous Layer CTF** — agent-only competition; OCI-containerized agents, centralized inference so nobody wins on GPU budget (full entry at `0x0E`).
- **AI Village Plays Pokémon: DEF CON Edition** — Nick Ashworth; novice-friendly local-model tooling competition and live demo.
- **Cyber Mirage: Real-Time Deepfake Demos** — Brandon Kovacs; open-source real-time voice and video impersonation on consumer hardware, all three days.
- **Fooling Coding Agents for Fun and Profit** — Jack Cable &amp; Matt Galligan (fireside).
- **Bruce's Fireside Chat** — Bruce Schneier, Saturday 1:00 PM.
- **What can those architecting agents learn from national security?** — David C Eight (UK NCSC AI Safety Institute).
- **MeshLens: Security Profiling at Scale** — Vipul Ujawane, Jigar Bhavsar, Rayden Chia (Google).
- **Federated AI Agent Community Forum &amp; DNS-AID Discovery Lab** — Ingmar Van Glabbeek &amp; Emily Soward.

Also on the DEF CON stages and not separately profiled above: *This Wasn't AI Generated: Principles for Breaking Generative Watermarks* (Thomas Mason &amp; Tahseen Rabbani), and *Leveraging Large Language Models for Policy, Regulatory, and Compliance in IoMT* (Dr. Deepti Gupta &amp; Sai Sitharaman).

<details>
<summary><b>&#9656; sources for this appendix</b></summary>

**AI Village @ DEF CON 34 — Full schedule, poster roster, and presentation times**  
<https://aivillage.org/events/defcon-34/>

**AI Village — Poster archive (files added as authors submit them)**  
<https://aivillage.org/posters/#defcon-34>

**AI Village @ DEF CON 34 — Call for Posters (theme: Adversarial Attacks Against Agents)**  
<https://easychair.org/cfp/aiv8>

</details>

---

## 0xFF :: MASTER SOURCES :: All URLs &amp; Original Content

Every source used, grouped by talk, in the format: **bold title above, link below.** Primary conference pages and researcher/vendor write-ups are favored over aggregators.

#### ▸ The CoreBreak Attack: Turning AI Agents into Credential Exfiltration Vectors

**Black Hat USA 2026 -- Session page (The CoreBreak Attack)**  
<https://blackhat.com/us-26/briefings/schedule/#the-corebreak-attack-turning-ai-agents-into-credentials-exfiltration-vectors-53825>

**The Hacker News -- AWS, Google, and Vercel Agent Flaws Let Attackers Trigger Tools Without Running the Model**  
<https://thehackernews.com/2026/08/aws-google-and-vercel-patch-agent-flaws.html>

**AWS Security Bulletin -- 2026-073 (CVE-2026-18830)**  
<https://aws.amazon.com/security/security-bulletins/2026-073-aws/>

#### ▸ Can AI Do Novel Security Research? Meet the HTTP Terminator

**PortSwigger Research -- Can AI do novel security research? Meet the HTTP Terminator (whitepaper)**  
<https://portswigger.net/research/can-ai-do-novel-security-research>

**Black Hat USA 2026 -- Session page**  
<https://blackhat.com/us-26/briefings/schedule/#can-ai-do-novel-security-research-meet-the-http-terminator-51894>

**Printable whitepaper PDF**  
<https://portswigger.net/kb/papers/gkaicuremal/http-terminator.pdf>

#### ▸ When AI Attacks AI: Inside the Self-Propagating Botnet Built on Compromised AI Infrastructure

**Forkast -- Black Hat USA 2026 Signals Agent Exploitation Has Become Its Own Infrastructure Discipline**  
<https://forkast.news/black-hat-usa-2026-signals-agent-exploitation-has-become-its-own-infrastructure-discipline/>

**Forkast -- Black Hat Day 1 Briefings Reveal the Agent Stack Is the Attack Surface**  
<https://forkast.news/black-hat-day-1-briefings-reveal-the-agent-stack-is-the-attack-surface/>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

#### ▸ No Tools Required: Post-Injection Exploitation Across AI Agent Frameworks

**Forkast -- Black Hat Day 1 Briefings Reveal the Agent Stack Is the Attack Surface**  
<https://forkast.news/black-hat-day-1-briefings-reveal-the-agent-stack-is-the-attack-surface/>

**Forkast -- Agent Exploitation Has Become Its Own Infrastructure Discipline**  
<https://forkast.news/black-hat-usa-2026-signals-agent-exploitation-has-become-its-own-infrastructure-discipline/>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

#### ▸ Cost-Effective, Private, Frontier-Grade: AI Agent Exploitation with a Fine-Tuned OSS Model

**Forkast -- Agent Exploitation Has Become Its Own Infrastructure Discipline**  
<https://forkast.news/black-hat-usa-2026-signals-agent-exploitation-has-become-its-own-infrastructure-discipline/>

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

#### ▸ Bye Bye AI: How We Hacked the AI Shopping Assistant of a Top-3 US Retailer

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Black Hat USA 2026 -- Session page (Bye bye AI)**  
<https://blackhat.com/us-26/briefings/schedule/#bye-bye-ai-how-we-hacked-the-ai-shopping-assistant-of-a-top-3-us-retailer-53360>

**LastPass -- Complete Guide to Black Hat USA 2026**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

#### ▸ ChatMate: Remote Prompt Execution on AI Assistants through Sandbox Escaping

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Black Hat USA 2026 -- Session page (ChatMate)**  
<https://blackhat.com/us-26/briefings/schedule/#chatmate-remote-prompt-execution-on-ai-assistants-through-sandbox-escaping-52326>

**LastPass -- Complete Guide to Black Hat USA 2026**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

#### ▸ Caging the Agent: How Roblox Built Multi-Layer Sandboxes to Secure Claude Code at Enterprise Scale

**Forkast -- From Lab Curiosity to Mainstream Threat: Black Hat USA 2026 and the Rise of AI Agent Security**  
<https://forkast.news/from-lab-curiosity-to-mainstream-threat-black-hat-usa-2026-and-the-rise-of-ai-agent-security/>

**Black Hat USA 2026 -- Session page (Caging the Agent)**  
<https://blackhat.com/us-26/briefings/schedule/#caging-the-agent-how-roblox-built-multi-layer-sandboxes-to-secure-claude-code-at-enterprise-scale-53708>

**CVE-2026-25725 -- Claude Code sandbox escape via settings.json (context)**  
<https://osv.dev/vulnerability/CVE-2026-25725>

#### ▸ A Billion-User Blast Radius: Owning ChatGPT's Secure Sandbox

**Dark Reading -- Researcher Claims Control of ChatGPT Secure Sandbox**  
<https://www.darkreading.com/cloud-security/researcher-claims-control-chatgpt-secure-sandbox>

**DEF CON 34 -- Creator Stage Talks listing**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**Black Hat USA 2026 -- Session page**  
<https://blackhat.com/us-26/briefings/schedule/#a-billion-user-blast-radius-owning-chatgpts-secure-sandbox-53432>

#### ▸ Pwning Agentic Browsers with PleaseFix: A New Vulnerability Class for 0-Click Takeover

**Zenity Labs -- PleaseFix: Zero-Click AI Agent Vulnerabilities**  
<https://zenity.io/research/pleasefix-vulnerabilities>

**Dark Reading -- AI Browsers Vulnerable to 'PleaseFix' Zero-Click Agent Hijacking**  
<https://www.darkreading.com/cyber-risk/ai-browsers-zero-click-agent-hijacking>

**DEF CON 34 AI Village -- Schedule**  
<https://aivillage.org/events/defcon-34/>

#### ▸ Pwning the Internet of Agents: Zero-Click Backdoors in OpenClaw and a Global Agent Botnet on MoltBook

**DEF CON 34 AI Village -- Schedule & Fireside Chats**  
<https://aivillage.org/events/defcon-34/>

**AI Village Poster -- Agent-to-Agent Worm Propagation in MCP-Based AI Systems**  
<https://aivillage.org/posters/agent-to-agent-worm-propagation-in-mcp-based-ai-systems/>

**AI Village @ DEF CON 34 -- overview**  
<https://aivillage.org/events/defcon-34/>

#### ▸ Keynote Panel: What is the Right Balance of Rules for Defenders & Adversaries?

**DEF CON 34 AI Village -- Schedule (Keynote Panel)**  
<https://aivillage.org/events/defcon-34/>

**AI Village @ DEF CON 34 -- overview**  
<https://aivillage.org/events/defcon-34/>

**Tech Times -- DEF CON 34 Opens: AI Agents Graduate From Novelty to Standard Hacking Weapon**  
<https://www.techtimes.com/articles/323346/20260806/def-con-34-opens-today-ai-agents-graduate-novelty-standard-hacking-weapon.htm>

#### ▸ HalCTF: Hostile Autonomous Layer CTF (+ the Autonomous-Agent Competition Arc)

**AI Village -- HalCTF: Hostile Autonomous Layer CTF**  
<https://aivillage.org/blog/halctf/>

**Tech Times -- DEF CON 34 Opens: AI Agents Graduate From Novelty to Standard Hacking Weapon**  
<https://www.techtimes.com/articles/323346/20260806/def-con-34-opens-today-ai-agents-graduate-novelty-standard-hacking-weapon.htm>

**AI Village @ DEF CON 34 -- Schedule**  
<https://aivillage.org/events/defcon-34/>

#### ▸ Attacking and Defending AI Browsers

**Dark Reading -- No Perfect Fix for AI Browser Prompt Injection Flaws**  
<https://www.darkreading.com/application-security/no-perfect-fix-ai-browser-prompt-injection-flaws>

**Black Hat USA 2026 -- Session page (Attacking and Defending AI Browsers)**  
<https://blackhat.com/us-26/briefings/schedule/#attacking-and-defending-ai-browsers-51657>

**Dark Reading -- AI Agents Undermine Progress in Browser Security**  
<https://www.darkreading.com/application-security/ai-agents-undermine-progress-browser-security>

#### ▸ Trusted Enough to Run: Breaking AI Agents in Official Workflows

**GlobeNewswire -- Novee Researchers to Present Four Sessions across Black Hat USA and DEF CON**  
<https://www.globenewswire.com/news-release/2026/07/28/3334295/0/en/Novee-Researchers-to-Present-Four-Sessions-across-Black-Hat-USA-and-DEF-CON-Uncovering-Vulnerabilities-in-Anthropic-OpenAI-and-Google.html>

**Novee -- Top 8 Black Hat 2026 Briefings for AI Offensive Security Leaders**  
<https://novee.security/blog/black-hat-2026-briefings-ai-offensive-security/>

**Dark Reading -- AI Harnesses Burst With Potential Exploit Opportunities**  
<https://www.darkreading.com/application-security/ai-harnesses-potential-exploit-opps>

#### ▸ No Prompt Required: Pre-Task RCE in Google Gemini CLI

**GlobeNewswire -- Novee Researchers to Present Four Sessions across Black Hat USA and DEF CON**  
<https://www.globenewswire.com/news-release/2026/07/28/3334295/0/en/Novee-Researchers-to-Present-Four-Sessions-across-Black-Hat-USA-and-DEF-CON-Uncovering-Vulnerabilities-in-Anthropic-OpenAI-and-Google.html>

**DEF CON 34 -- Creator Stage / Talk listings**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**Novee Security -- Labs & research index**  
<https://novee.security/blog/category/novee-labs/>

#### ▸ The Sandbox Is a Suggestion: Deconstructing AI Agent Sandboxes

**GlobeNewswire -- Novee Researchers to Present Four Sessions across Black Hat USA and DEF CON**  
<https://www.globenewswire.com/news-release/2026/07/28/3334295/0/en/Novee-Researchers-to-Present-Four-Sessions-across-Black-Hat-USA-and-DEF-CON-Uncovering-Vulnerabilities-in-Anthropic-OpenAI-and-Google.html>

**OSV -- CVE-2026-25725: Claude Code sandbox escape via persistent configuration injection**  
<https://osv.dev/vulnerability/CVE-2026-25725>

**NVIDIA -- Practical Security Guidance for Sandboxing Agentic Workflows and Managing Execution Risk**  
<https://developer.nvidia.com/blog/category/cybersecurity>

#### ▸ One Percent of the Tokens, All of the Strategy: LLM-Assisted Vulnerability Discovery in IoT and Embedded Firmware

**Black Hat USA 2026 -- Session page (One Percent of the Tokens)**  
<https://blackhat.com/us-26/briefings/schedule/#one-percent-of-the-tokens-all-of-the-strategy-llm-assisted-vulnerability-discovery-in-iot-and-embedded-firmware-53075>

**LastPass -- Complete Guide to Black Hat USA 2026 (session listing)**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

**Onit Security -- Black Hat 2026: The Real Theme Is Speed**  
<https://onit.security/blog/black-hat-2026-briefings-forecast/>

#### ▸ Catch Me If You Can: AI Investigators Hunting Autonomous Attackers as a Benchmark

**Black Hat USA 2026 -- Session page (Catch Me If You Can)**  
<https://blackhat.com/us-26/briefings/schedule/#catch-me-if-you-can-ai-investigators-hunting-autonomous-attackers-as-a-benchmark-53869>

**Onit Security -- Black Hat 2026: The Real Theme Is Speed**  
<https://onit.security/blog/black-hat-2026-briefings-forecast/>

**LastPass -- Complete Guide to Black Hat USA 2026 (session listing)**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

#### ▸ Rules for Neural Traffic: A New Defensive Layer for LLMs

**Black Hat USA 2026 -- Session page (Rules for Neural Traffic)**  
<https://blackhat.com/us-26/briefings/schedule/#rules-for-neural-traffic-a-new-defensive-layer-for-llms-53675>

**LastPass -- Complete Guide to Black Hat USA 2026 (session listing)**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

**Black Hat USA 2026 -- Briefings**  
<https://blackhat.com/us-26/briefings.html>

#### ▸ The AI-Assisted Discovery Cluster: 0-Day Engine / Prompt2Own / Beyond Detection / Closed Loop

**Onit Security -- Black Hat 2026: The Real Theme Is Speed**  
<https://onit.security/blog/black-hat-2026-briefings-forecast/>

**Black Hat USA 2026 -- Briefings Schedule (official)**  
<https://blackhat.com/us-26/briefings/schedule/index.html>

**LastPass -- Complete Guide to Black Hat USA 2026**  
<https://blog.lastpass.com/posts/your-complete-guide-to-black-hat-usa-2026>

#### ▸ Kinetic Prompt Injection: Jailbreaking a Robot Dog Through Its Own Eyes and Ears

**UNAPOLOGETICALLY DAHLING -- Why Is the Scariest Morning at Black Hat 2026 a Thursday at 10:15?**  
<https://unapologeticallydahling.com/blog/black-hat-2026-the-most-terrifying-morning-in-vegas>

**Black Hat USA 2026 -- Briefings Schedule (official)**  
<https://blackhat.com/us-26/briefings/schedule/index.html>

**TIME -- Unitree Robotics (Go2 platform, pricing and deployment context)**  
<https://www.aol.com/unitree-robotics-112824308.html>

#### ▸ The Silent Participant: AI Notetaker Exposure Across Government and Corporate Video Calls

**Dark Reading -- AI Notetaker Lets Hackers Spy on Government, Corporate Video Calls**  
<https://www.darkreading.com/application-security/ai-notetaker-spy-government-corporate-video-calls>

**BobDaHacker -- tl;dv research write-up**  
<https://bobdahacker.com/blog/tldv-hack>

**Brinztech -- AI Meeting Assistant Vulnerabilities Expose Corporate and Government Video Calls**  
<https://www.brinztech.com/breach-alerts/brinztech-alert-ai-meeting-assistant-vulnerabilities-expose-corporate-and-government-video-calls>

#### ▸ That's Not Your Agent: Why Zero Trust Can't Tell (+ the Identity Boundary Cluster)

**AI Village @ DEF CON 34 -- Schedule (Saturday DEF CON stage sessions)**  
<https://aivillage.org/events/defcon-34/>

**DEF CON 34 -- Creator Stage Talks (official)**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**AI Village -- Poster archive (identity & governance posters)**  
<https://aivillage.org/posters/>

#### ▸ Minimize Harm, Maximize Defense: How Anthropic Navigates the Offense-Defense Divide (+ the SATAN Retrospective)

**AI Village @ DEF CON 34 -- Schedule (Saturday DEF CON stage sessions)**  
<https://aivillage.org/events/defcon-34/>

**DEF CON 34 -- Creator Stage Talks (official)**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**Dark Reading -- Anthropic: Claude Attacks Result of Security Gaps, Not Model Issues**  
<https://www.darkreading.com/cyber-risk>

#### ▸ Scaling Adversary Emulation with Autonomous Agents (+ AgentBreaker & MeshLens)

**AI Village @ DEF CON 34 -- Schedule (Friday & Saturday sessions)**  
<https://aivillage.org/events/defcon-34/>

**Dark Reading -- AI Harnesses Burst With Potential Exploit Opportunities**  
<https://www.darkreading.com/application-security/ai-harnesses-potential-exploit-opps>

**DEF CON 34 -- Creator Stage Talks (official)**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

### ▚ PRIMARY INDEX / SCHEDULES

**Black Hat USA 2026 — Briefings (official)**  
<https://blackhat.com/us-26/briefings.html>

**Black Hat USA 2026 — Briefings Schedule (official)**  
<https://blackhat.com/us-26/briefings/schedule/index.html>

**DEF CON 34 — AI Village (schedule, posters, competitions)**  
<https://aivillage.org/events/defcon-34/>

**DEF CON 34 — Creator Stage Talks (official)**  
<https://defcon.org/html/defcon-34/dc-34-creator-talks.html>

**PortSwigger Research — Upcoming Talks (HTTP Terminator listing)**  
<https://portswigger.net/research/talks>

**Forkast — Black Hat Day 1: The Agent Stack Is the Attack Surface**  
<https://forkast.news/black-hat-day-1-briefings-reveal-the-agent-stack-is-the-attack-surface/>

**Tech Times — DEF CON 34 Opens: AI Agents Graduate to Standard Hacking Weapon**  
<https://www.techtimes.com/articles/323346/20260806/def-con-34-opens-today-ai-agents-graduate-novelty-standard-hacking-weapon.htm>

---

<div align="center">

```
        ___________________________________
       |  [ end of file ]  keep it ethical |
       |    0 d a y   i s   f o r e v e r   |
       |___________________________________|
```

**EOF** // -=[ compiled defanged for research &amp; education ]=- // stay curious, stay legal

</div>
