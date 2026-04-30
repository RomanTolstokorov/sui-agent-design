# S-System: Product Opportunities
### Executive Briefing — April 2026

---

## Executive Summary

S-System is a 6-year-old government correspondence and case management platform handling document workflows, task tracking, and organizational record management. The platform is **technically capable but commercially underutilized**: a full AI stack (LLM backend, vector search, NER pipeline, streaming APIs) is deployed and partially operational, but key user-facing connections are missing or incomplete.

**The core finding:** the platform has already paid the infrastructure cost of advanced AI and analytics capabilities. The highest-value opportunities require connecting existing backend services to the user interface — not building from scratch.

**3 priorities for immediate ROI:**

1. **Wire AI tools into the document editor** — backend endpoints exist and are tested; the UI connection is absent.
2. **Build operational reporting** — all data lives in Elasticsearch; the platform lacks the query and visualization layer that makes it useful to management.
3. **Add multi-channel notifications** — users who are not logged in receive zero alerts, making the platform invisible outside working hours.

---

## Platform Snapshot

| Dimension | Current State |
|---|---|
| Core function | Document lifecycle, task management, government correspondence |
| Architecture | Java/Kotlin microservices + React SPA + Python AI service |
| Data stores | MongoDB (documents), Elasticsearch (search/analytics), Qdrant (AI vector), Redis (sessions) |
| AI services deployed | RAG chat, NER extraction, document summarization, text tools (improve/rewrite/autocorrect/subject), variation generation |
| Users | Government agents managing correspondence, admins, supervisors |
| Key integration | Jira (task state authority), Keycloak (SSO), external e-service (AI tools host) |
| Platform age | 6+ years, active development |
| Documented features | 70+ across backend, frontend, and DevOps |

---

## Opportunity 1 — Inline AI Writing Tools

### Problem
Agents write government correspondence in a rich text editor. AI text tools (improve writing, auto-correct, generate subject, summarize) exist as live streaming API endpoints. The editor does not call them. Agents write without AI assistance despite the capability being deployed.

### What Exists Today
- `/improve` — rewrites text with optional custom instruction
- `/auto-correct` — fixes spelling, grammar, punctuation
- `/summary` — generates a concise summary
- `/subject` — generates a short subject/topic phrase
- All served as Server-Sent Events (SSE) from the AI backend
- Config per document type/subtype stored in `preferences` service

### What Is Missing
A toolbar in the rich text editor that invokes these endpoints on selected text and streams the result back inline. The backend is ready. The frontend is not connected.

### User Benefit
Agents produce higher-quality correspondence faster. Fewer revision cycles. Consistent language across documents of the same type.

### Business Benefit
Reduced time-per-document. Measurable quality improvement via existing `ai_generated` / `ai_reviewed` flags. Low implementation cost — backend work is complete.

### Effort
**Low.** Frontend work only. No new services required.

---

## Opportunity 2 — AI Chat Connected to Internal Corpus

### Problem
The AI chat assistant (aibot) runs as a separate embedded service with its own isolated knowledge store (Qdrant). Users can upload files to give it context, but it cannot query S-System's live document and record database. Agents asking "what was the outcome of task X?" or "which documents involve person Y?" get no answer from the chat.

### What Exists Today
- Full RAG pipeline: Qdrant vector store, document ingestion, streaming completions
- MCP tool integration inside the chat model
- SSO session bridge from S-System to aibot
- Elasticsearch indices holding all documents, tasks, records, and their metadata

### What Is Missing
MCP tools or direct retrieval adapters that let the AI query S-System's Elasticsearch indices. Users would then get answers grounded in live system data, not just uploaded attachments.

### User Benefit
The AI assistant becomes genuinely useful for day-to-day work — finding documents, surfacing task history, answering questions about entities — rather than being a generic chatbot.

### Business Benefit
Reduces time spent on manual search. Increases AI chat adoption rate, which justifies the infrastructure cost already spent. Positions the platform as an AI-native case management system.

### Effort
**Medium.** Requires implementing MCP search tools in aibot and mapping them to the S-System search API. No new infrastructure.

---

## Opportunity 3 — AI Feedback Loop (Ratings → Quality)

### Problem
Users can rate AI answers with like/dislike and an optional comment. This signal is collected and stored. There is no documented pathway from this data to model improvement, prompt tuning, or quality metrics.

### What Exists Today
- Per-message rating stored in aibot
- Variation selection history (which AI reply the agent chose)
- `ai_reviewed` flag on documents (agent verified AI content)

### What Is Missing
A pipeline that aggregates ratings and selections into quality metrics, surfaces them to administrators, and feeds preferred examples into prompt tuning or model selection decisions.

### User Benefit
AI outputs get better over time. Agents notice the system learning from their corrections.

### Business Benefit
Demonstrates measurable AI quality improvement to the client. Differentiates the platform from commodity AI integrations. Enables data-driven LLM vendor decisions.

### Effort
**Medium.** Analytics pipeline and admin reporting view. Model fine-tuning is optional and additive.

---

## Opportunity 4 — Variation Auto-Ranking

### Problem
The Variation Center is an inbox where agents manually review every AI-generated reply document alternative for a task. There is no scoring, no ranking, and no filtering by predicted quality. Agents with many tasks browse through all variants to find the best one.

### What Exists Today
- Variations stored with priority scores, entity filters, read/unread state, favourite flag
- Manual summary generation and multi-report summarization
- User selection history (which variation was chosen)

### What Is Missing
A ranking model — even a simple one based on past selection patterns — that surfaces the most likely-useful variation at the top of the inbox.

### User Benefit
Agents find the right AI reply faster. Reduces cognitive load on high-volume task queues.

### Business Benefit
Increases throughput per agent. Demonstrates measurable productivity gain. Reuses existing variation data without new data collection.

### Effort
**Medium.** Ranking logic in taskmanagement service + UI sort order change.

---

## Opportunity 5 — Operational Reporting and SLA Dashboard

### Problem
The Dashboard has four Jira tickets in its entire history. It renders Elasticsearch aggregations as counters with a feature-flagged classifications tab. There are no time-series charts, no SLA tracking, no per-user or per-group performance metrics, and no export. A "Reports" section appears in the navigation bar but has no corresponding documented feature.

### What Exists Today
- All documents, tasks, transitions, and history indexed in Elasticsearch
- Aggregation queries in the search service
- Classification data per document/task
- Full audit trail of admin actions
- Task assignment history

### What Is Missing
A reporting layer: time-series queries, per-group breakdowns, SLA threshold configuration, and a visualization/export interface.

### Metrics That Could Be Served Today (data already exists)

| Metric | Source |
|---|---|
| Tasks created / resolved per day | Elasticsearch task index |
| Average time-in-state per task type | Task transition history |
| Documents submitted per group per week | Document index |
| Discovery access requests granted vs. denied | Search service |
| AI variation acceptance rate | Variation selection data |
| Top document types by volume | Document index aggregation |

### User Benefit
Supervisors and managers get visibility into team performance without exporting data manually. Agents can see their own metrics.

### Business Benefit
Satisfies typical government audit and performance review requirements. Positions the platform for SLA-based contracts. Makes the platform stickier for management stakeholders beyond frontline agents.

### Effort
**Medium.** Query and visualization work. No new data collection required.

---

## Opportunity 6 — Deadline-Based Workflow Escalation

### Problem
The orchestrator triggers only on Jira state-change callbacks. If a task sits in an intermediate state for days or weeks, nothing happens automatically. There are no time-based alerts, no auto-reassignment, and no escalation rules. A Quartz scheduler service is deployed but only used for file cleanup.

### What Exists Today
- Quartz scheduler (running, deployed, with maintenance jobs)
- Full task state and assignment history in taskmanagement
- Real-time notification delivery infrastructure (WebSocket/STOMP)
- Configurable task types and workflow transitions

### What Is Missing
Scheduler jobs that inspect task age by state and trigger notifications or reassignments when thresholds are exceeded.

### User Benefit
No task falls through the cracks silently. Agents are reminded of stalled work. Supervisors are alerted to bottlenecks before they escalate.

### Business Benefit
Reduces case backlog risk. Enables SLA commitments backed by automated enforcement. Reuses deployed infrastructure — no new services.

### Effort
**Medium.** New Quartz jobs + notification events. Threshold configuration UI can ship in a later iteration.

---

## Opportunity 7 — Multi-Channel Notifications

### Problem
Notifications are delivered exclusively over WebSocket/STOMP to the browser. Users who are not logged into S-System receive no alerts. Task assignments, document shares, and discovery access decisions are invisible to off-platform users.

### What Exists Today
- Typed notification event system: task assigned, document submitted, list refresh, etc.
- User profile and contact information in user-management
- Notification service as a dedicated microservice

### What Is Missing
Adapters for email (and optionally push/SMS) delivery, plus user-level notification preference settings.

### User Benefit
Agents receive task notifications even when not actively using the application. Response time improves. Critical approvals are not missed.

### Business Benefit
Reduces missed deadlines caused by absent users. Expands the platform's effective reach beyond the office browser session. Expected by users of any modern enterprise system.

### Effort
**Medium.** New notification adapters + preferences UI. Email is the highest-priority channel.

---

## Opportunity 8 — Access Governance Visibility

### Problem
The security model is the most sophisticated part of S-System: ACL, DCL, discovery access tokens, temporary access, classification roles, and shared group lists. All of it is enforced correctly. None of it is visible in aggregate. Admins cannot answer "who can currently see document X?" without querying the database directly.

### What Exists Today
- All access data stored in search service (tokens) and insert service (ACLs)
- Full audit trail of ACL changes
- Bulk grant/deny for discovery access
- Revoke conflicting tokens capability

### What Is Missing
An admin-facing access visibility dashboard and automated expiry alerts for discovery access tokens.

### User Benefit
Admins can audit and clean up access without engineering support.

### Business Benefit
Satisfies government compliance and security review requirements. Reduces risk of over-permissioned documents. Demonstrates security posture to auditors.

### Effort
**Medium.** Read-only admin dashboard querying existing data.

---

## Opportunity 9 — Autolinking Disambiguation

### Problem
The NER autolinking pipeline extracts entities from documents and attempts to match them to records. When it finds zero matches or too many matches, it silently stops. No user is informed. No recovery path exists.

### What Exists Today
- NER pipeline running on document submission
- Autolinking result codes: `SUCCESS`, `NO_CANDIDATES_FOUND`, `TOO_MANY_CANDIDATES`
- Record search infrastructure to find candidates

### What Is Missing
A disambiguation UI that surfaces unresolved entity links to the agent, shows the top candidates, and lets the agent confirm or skip.

### User Benefit
Agents can complete record linkage the NER pipeline couldn't resolve. Document records become more complete and accurate.

### Business Benefit
Improves data quality across the record database. Increases the value of indexed data for search and analytics.

### Effort
**Low.** UI modal + simple API call to search with entity value. No new backend infrastructure.

---

## Opportunity 10 — Arabic Machine Translation Pipeline

### Problem
The platform is built for Arabic government workflows. UI translations are managed manually: administrators upload JSON translation maps. There is no automated translation of document content. Agents drafting in English must translate manually before sending.

### What Exists Today
- OpenAI-compatible LLM backend already deployed (used for chat, summarization, text tools)
- Admin translation management UI (upload/edit translation maps)
- RTL layout throughout the application
- Arabic NER pipeline

### What Is Missing
A translation endpoint using the deployed LLM, with output routed through the admin review workflow before publication.

### User Benefit
Agents can draft in either language and produce a version in the other without leaving the platform.

### Business Benefit
Expands the platform's utility to bilingual workflows. LLM infrastructure cost is already paid.

### Effort
**Low.** New endpoint in the AI backend + minimal UI entry point. Admin review workflow already exists.

---

## Feature Benefit Analysis

| Opportunity | Primary Beneficiary | Business Impact | User Impact | Infra Ready? | Effort |
|---|---|---|---|---|---|
| 1. Inline AI writing tools | Agents | High | High | Yes — endpoints exist | Low |
| 9. Autolinking disambiguation | Agents | Medium | Medium | Yes | Low |
| 10. Arabic machine translation | Agents, Admins | Medium | Medium | Yes — LLM deployed | Low |
| 5. Operational reporting / SLA | Supervisors, Admins | High | High | Yes — data in ES | Medium |
| 6. Deadline-based escalation | Supervisors, Agents | High | High | Yes — Quartz deployed | Medium |
| 7. Multi-channel notifications | Agents | High | High | No | Medium |
| 2. AI chat + internal corpus | Agents | High | High | Partially | Medium |
| 3. AI feedback loop | Admins, Product | Medium | Low (indirect) | Yes — data exists | Medium |
| 4. Variation auto-ranking | Agents | Medium | Medium | Yes | Medium |
| 8. Access governance dashboard | Admins | Medium | Low (admin only) | Yes — data exists | Medium |

---

## Recommended Sequencing

### Phase 1 — Quick Wins (1–4 weeks each)
No new infrastructure. Deliver visible user value immediately.

1. **Inline AI text tools** — connect existing SSE endpoints to the editor toolbar
2. **Autolinking disambiguation UI** — surface unresolved entity links with candidate list
3. **Arabic machine translation endpoint** — one new API route using the deployed LLM

### Phase 2 — Structural Improvements (1–3 months each)
New logic required, but builds entirely on existing data and deployed services.

4. **Operational reporting + SLA dashboard** — Elasticsearch queries + visualization layer
5. **Deadline-based workflow escalation** — new Quartz jobs + notification events
6. **AI feedback loop pipeline** — aggregate ratings into quality metrics and admin view

### Phase 3 — Platform Expansion (3–6 months)
Opens new user segments or market capabilities.

7. **Multi-channel notifications** — email adapter + user preferences
8. **AI chat grounded in internal corpus** — MCP tools connecting aibot to S-System search
9. **Access governance visibility dashboard** — admin read view of ACL/token state
10. **Variation auto-ranking** — ranking model based on agent selection history

---

## Closing Note

S-System has the technical depth of a platform that cost significantly more to build than most clients recognize. The AI services, workflow engine, search infrastructure, and security model are all production-grade. The opportunity is in **completing the last mile** — connecting what is already deployed to what users actually see and do every day. Phase 1 alone requires no new infrastructure investment and could deliver measurable improvement within weeks.
