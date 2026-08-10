# AI-103 — 8-Week Study Plan
**Exam:** AI-103 *Developing AI Apps and Agents on Azure* → Microsoft Certified: Azure AI Apps and Agents Developer Associate
**Booked:** Thursday 9 October 2026 · **Start:** Monday 10 August 2026 · **Budget:** 2–3 h/day

---

## Exam facts (from Microsoft Learn)

| Item | Detail |
|---|---|
| Duration | 120 minutes |
| Passing score | 700 / 1000 (scaled) |
| Format | Proctored, scenario-based, may include interactive components |
| Language requirement | Python |
| **Open book** | Microsoft Learn is accessible during the exam (learn.microsoft.com only — Q&A forums, practice assessments and your profile are blocked). **The timer keeps running.** |
| Official practice assessment | **Not available yet** for AI-103 — check the cert page periodically |
| Exam sandbox | https://aka.ms/examdemo — free, try the question UI |
| Retake | Allowed 24 h after a first failure |

### Domain weights → where your hours go

| # | Domain | Weight | Target hours |
|---|---|---|---|
| 2 | Implement generative AI and agentic solutions | **30–35%** | ~35 h |
| 1 | Plan and manage an Azure AI solution | **25–30%** | ~28 h |
| 5 | Implement information extraction solutions | 10–15% | ~14 h |
| 3 | Implement computer vision solutions | 10–15% | ~12 h |
| 4 | Implement text analysis solutions | 10–15% | ~12 h |
| — | Azure platform ramp-up (your personal gap) | n/a | ~10 h |
| — | Practice tests + weak-area repair | n/a | ~15 h |

Domains 1 + 2 = **55–65% of the exam.** Do not split your time evenly across five domains.

---

## Core resources

**Official (the backbone):**
- Study guide (the authoritative objective list): https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103
- Learning path — Get started with AI applications and agents: https://learn.microsoft.com/en-us/training/paths/get-started-ai-apps-agents/
- Learning path — Develop generative AI apps: https://learn.microsoft.com/en-us/training/paths/develop-generative-ai-apps-azure/
- Learning path — Develop AI agents on Azure: https://learn.microsoft.com/en-us/training/paths/develop-ai-agents-azure/
- Learning path — Develop natural language solutions: https://learn.microsoft.com/en-us/training/paths/develop-natural-language-solutions-azure/
- Learning path — Extract insights from visual data: https://learn.microsoft.com/en-us/training/paths/extract-insights-visual-data-azure/
- Learning path — Develop AI information extraction solutions: https://learn.microsoft.com/en-us/training/paths/ai-extract-information/

**Official lab repos (MicrosoftLearning org — the real hands-on material):**
- https://github.com/MicrosoftLearning/mslearn-ai-agents (hosted instructions: https://microsoftlearning.github.io/mslearn-ai-agents/)
- https://github.com/MicrosoftLearning/mslearn-ai-information-extraction
- https://github.com/MicrosoftLearning/ai-apps

**Third-party (supplementary only):**
- Community study guide (unofficial, ~5 stars, self-declared "not official exam material"): https://github.com/pratip-bagchi/ai-103-study-guide — good for end-of-week review and for its mind map, bad as a primary source.
- Practice question banks (Udemy / Examinotion / Tutorials Dojo) — pick **one**, only from week 4 onward.

---

## Day 0 setup checklist — do this before studying anything

- [ ] **Get an Azure subscription with credit.** Apply for Azure for Students with your `@miuandes.cl` address (no credit card needed if you qualify): https://azure.microsoft.com/free/students. If that fails, use the standard free account with its 30-day credit.
- [ ] Register your Microsoft Learn profile with the **same personal MSA account** you used at Pearson VUE.
- [ ] Confirm your booking shows the voucher applied, and decide now: **test centre or online proctored.** Online needs a clean room, a photo ID, and a passed system check — run the check this week, not on 8 October.
- [ ] Create one resource group, e.g. `rg-ai103`, and put **everything** in it. At the end of every lab session: delete or deallocate. Foundry model deployments burn credit while idle.
- [ ] Set a budget alert on the subscription at ~50% of your credit.
- [ ] Local env: Python 3.11+, VS Code, Azure CLI (`az login`), and a `.venv` per lab.
- [ ] Open the exam sandbox once (https://aka.ms/examdemo) just to see the question types.
- [ ] Start a file called `decisions.md`. Explained below — it is the single most valuable thing you will produce.

---

## The `decisions.md` habit

You already know AI. What AI-103 actually tests is **"given this scenario, which Azure/Foundry thing do I pick?"** So every time you meet a new service, add one row:

| Service | Use it when | Do NOT use it when | Confused with |
|---|---|---|---|
| Azure AI Search (agentic retrieval) | Grounding an agent in private data; hybrid/vector/semantic search | You need the agent runtime itself | Foundry Agent Service |
| Foundry Agent Service | You need the runtime that hosts agents, tools, threads | You need designed multi-step flow control | Prompt Flow, Agent Framework |
| Content Understanding | Multimodal / unstructured extraction across docs, images, audio, video | Highly structured templated forms at max accuracy | Document Intelligence |
| Document Intelligence | Structured forms, tables, key-value pairs via OCR + layout | Audio, video, free-form multimodal input | Content Understanding |
| RAG | Answers must be grounded in private/current data | You need to change tone, format, or behaviour | Fine-tuning |
| Fine-tuning | Adapting style, format, or task behaviour | Injecting knowledge the model lacks | RAG |

Add ~5 rows a week. By week 7 this table *is* your revision. It is also what you'd look up during the open-book exam — but you should know it well enough that you rarely need to.

---

## Week 1 — Aug 10–16 · Azure platform ramp-up
*Your real gap is not AI. It's Azure's resource model and naming.*

- Learning path: **Get started with AI applications and agents on Azure** (whole thing)
- Concepts to nail: subscription → resource group → resource; regions and why model availability varies; **Microsoft Entra ID**; **managed identity vs keys** (AI-103 pushes keyless); RBAC roles; quotas and TPM rate limits.
- Foundry structure: what a **Foundry resource** vs a **Foundry project** is, and what a project endpoint gives you.
- **Hands-on:** create a Foundry project, deploy one chat model, call it from Python with the Foundry SDK using `DefaultAzureCredential` (not an API key).
- **AWS translation exercise** (30 min, do it once): map IAM→Entra/RBAC, S3→Blob Storage, Bedrock→Foundry Models, Kendra/OpenSearch→AI Search, Textract→Document Intelligence. Then *stop* thinking in AWS terms — the exam does not reward analogies.
- ⚠️ Vocabulary trap: Azure AI Studio and Azure AI Foundry are now **Microsoft Foundry**; bundled Azure AI Services are now **Foundry Tools**. Any tutorial using the old names predates this exam.

**End of week:** you can create a project, deploy a model, and call it from Python without a tutorial open.

---

## Week 2 — Aug 17–23 · Generative AI apps + RAG (Domain 2, part 1)

- Learning path: **Develop generative AI apps** (whole thing)
- Topics: deploying LLMs / SLMs / code models / multimodal models; prompt engineering and model parameters; **implementing RAG in an application**; evaluating apps (groundedness, relevance, fluency, fabrication detection); connecting an app to a Foundry project.
- **Hands-on:** build one working RAG chat app end to end — chunk a document set, index it, retrieve, ground, answer. Then break it deliberately: bad chunk size, no reranking, wrong top-k. Observe what degrades.
- `decisions.md`: RAG vs fine-tuning, embedding model choice, when to use an SLM.

**End of week:** a RAG app you wrote yourself, running.

---

## Week 3 — Aug 24–30 · Agents, part 1 (Domain 2, part 2)

- Learning path: **Develop AI agents on Azure** (first half)
- Topics: Foundry Agent Service; agent roles, goals, instructions; **tool schemas and function calling**; conversation memory / threads; knowledge tools (search, Content Understanding, MCP servers).
- **Hands-on:** an agent with (a) a custom Python function tool, (b) a retrieval tool over your week-2 index. Trace one full request end to end and read the trace.
- `decisions.md`: agent vs workflow vs plain function call — *knowing when NOT to use an agent is explicitly tested.*

---

## Week 4 — Aug 31–Sep 6 · Agents, part 2 + first diagnostic

- Learning path: **Develop AI agents on Azure** (second half) + repo `mslearn-ai-agents` labs
- Topics: multi-agent orchestration and handoff patterns (Microsoft Agent Framework); autonomous vs semi-autonomous workflows; **approval flows and safeguards**; observability — tracing, token analytics, latency breakdown; error analysis on agent behaviour.
- **Hands-on:** a two-agent solution with a human approval gate before one tool fires.
- **📊 Diagnostic (Sat):** take your first practice test, timed, 120 min, no notes. Expect a bad score — that's the point. Log every wrong answer by *domain* and by *reason* (didn't know the service / misread the scenario / knew it but rushed).

**Midpoint check:** Domain 2 is done. It's the biggest slice and the hardest to cram, so it's deliberately front-loaded.

---

## Week 5 — Sep 7–13 · Plan, manage, secure, govern (Domain 1)

*Second-biggest domain, and mostly Azure plumbing rather than AI — this is where your gap is widest.*

- Topics: choosing models and Foundry services per task; deployment options; **CI/CD integration for Foundry projects**; quotas, scaling, rate limits, cost footprint; monitoring drift, safety events, grounding quality, index health.
- Security: managed identity, private networking / private endpoints, **keyless credentials**, role policies.
- Responsible AI **at configuration depth, not principle level**: content filter categories and severity thresholds, prompt shields (indirect injection), protected material detection, evaluators and safety evaluations, trace logging, provenance metadata, oversight modes, tool-access controls.
- **Hands-on:** configure a custom content filter with non-default severities and prove it blocks what you expect; run a safety evaluation on your week-2 app; set up a managed identity so the app has zero keys in code.
- ⚠️ The exam asks *which filter category at which severity blocks this content* — not *why is responsible AI important*.

---

## Week 6 — Sep 14–20 · Vision + text/speech (Domains 3 & 4)

Two smaller domains, ~half a week each.

**Vision (Mon–Wed):** learning path *Extract insights from visual data*
- Image generation and editing (inpainting, mask-based edits); video generation and editing; multimodal image understanding, captioning, visual Q&A; **accessibility alt-text**; Content Understanding single-task vs **pro mode**; object/region identification.
- Responsible AI for visuals: unsafe-content classification, **indirect prompt injection via text embedded in images**, watermarking and brand/symbol policy rules.

**Text & speech (Thu–Sat):** learning path *Develop natural language solutions*
- LLM-based entity/topic/summary extraction and **structured JSON output**; sentiment, tone, PII/sensitive content detection; Azure Translator vs LLM-powered translation; domain customisation.
- Speech: STT and TTS **as an agent modality**, custom speech models, audio-native multimodal reasoning, speech translation.
- ⚠️ Candidates skip speech because it feels peripheral. It's an explicitly listed skill. Don't donate those marks.

---

## Week 7 — Sep 21–27 · Information extraction (Domain 5) + full mock

- Learning path: **Develop AI information extraction solutions** + repo `mslearn-ai-information-extraction`
- Topics: ingesting and indexing documents, images, audio, video; **semantic vs hybrid vs vector search**; skillsets and enrichment (built-in and custom); RAG ingestion flow including OCR; connecting retrieval pipelines to agent tools.
- Document extraction: OCR + layout + field extraction pipelines; Content Understanding analyzers producing structured/markdown output for downstream reasoning.
- ⚠️ **Content Understanding vs Document Intelligence** is a known trap. Content Understanding is new to AI-103 and handles multimodal/unstructured; Document Intelligence is the structured-forms specialist. Write the boundary in your own words in `decisions.md`.
- **📊 Full mock (Sat), timed.** Target: 70%+.

---

## Week 8 — Sep 28–Oct 4 · Consolidation

No new material. Repair only.

- **Mon–Tue:** rebuild every wrong answer from both mocks. For each, write one sentence: *why the right answer is right and why the distractor is tempting.*
- **Wed:** re-read the official study guide bullet by bullet. For every bullet you can't explain aloud in 30 seconds, that's your list.
- **Thu:** clear that list. Hands-on if it's a "how", `decisions.md` if it's a "which".
- **Fri:** second full mock, timed. Want 80%+.
- **Sat:** **open-book drills.** Give yourself 10 objectives and find each in learn.microsoft.com in under 60 seconds. You get Learn access in the exam but the clock keeps ticking, so the skill is *fast navigation*, not reading. Learn where the Foundry docs, Content Understanding docs, and AI Search docs live.
- **Sun:** rest. Genuinely.

---

## Oct 5–8 · Taper

- **Mon–Tue:** ~1 h/day. Read `decisions.md` only. No new content, no labs.
- **Wed:** logistics — confirm the booking email, test the Pearson VUE system check again if online, locate your ID, check the venue route if in person.
- **Thu 8th:** nothing. Sleep 8 hours.
- **Fri 9th:** exam. 120 min, ~50 questions ≈ 2.3 min each. **Flag and move on** — don't spend 6 minutes on question 4. Do a Learn lookup only for flagged items, and only on the second pass.

---

## The six most common ways people fail this exam

1. Blurring Foundry components — model deployment vs Agent Service vs Prompt Flow vs AI Search all seem plausible in a scenario.
2. Picking Document Intelligence when the scenario is multimodal (it wants Content Understanding).
3. Learning responsible AI as principle instead of as configuration.
4. Choosing fine-tuning where the scenario needs RAG.
5. Using AI-102-era material — anything mentioning Azure AI Studio as a standalone portal, LUIS, the Assistants API, or Azure Bot Service is stale.
6. Spreading study time evenly and under-preparing the 30–35% agentic domain.

---

## Weekly self-check

Every Sunday, 15 minutes, answer honestly:

- Did I hit ~15 hours? If not, which day leaked, and why?
- Can I build last week's hands-on thing again from scratch, without the lab guide?
- How many rows did `decisions.md` gain?
- What's the one thing I'm quietly avoiding? Do it Monday.
