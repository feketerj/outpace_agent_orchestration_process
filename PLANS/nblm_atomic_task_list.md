# NBLM Integration & Trust Framework — Atomic Task List

**Purpose:** Translate current research notes (`NOTES/` directory) into actionable, atomic tasks for orchestrating NBLM outputs, trust scoring, and model governance. Each task aligns with the user's "slow, safe, correct" maxim and maintains >95% confidence via explicit validation gates.

| ID | Task Description | Owner | Dependencies | Output / Artifact | Source Notes |
|----|------------------|-------|--------------|-------------------|--------------|
| 1.0 | Create `NBLM_OUTPUTS/` and `ORCHESTRATION_LOGS/` directories with access controls | Strategist Agent | Repository write access | Folder structure with read/write audit log | PRD §7 (F1.3), §18 |
| 1.1 | Document directory permissions and retention policy for NBLM data | Strategist Agent | Task 1.0 | `PLANS/nblm_data_retention.md` draft | PRD §12, Open Question #7 |
| 2.0 | User exports latest NBLM package (NotebookLM or other) to secure local staging path | User Action | NBLM access credentials | Raw NBLM payloads (`.json`, `.md`, `.txt`) | Perplexity Notes (Framework Research Layer) |
| 2.1 | User copies staged payload into `NBLM_OUTPUTS/inbox/SESSION_<timestamp>/raw/` | User Action | Task 1.0 | Timestamped raw payload directory | PRD §7 (F1.1) |
| 3.0 | Ingestion agent scans `inbox/` for new payloads and records metadata stub | Automation Agent | Tasks 1.0, 2.1 | `ORCHESTRATION_LOGS/SESSION_<timestamp>/ingestion_manifest.json` | PRD §7 (F1.1) |
| 3.1 | Classify payload type (strategy, requirements, code, research, data) using trust dimensions | Automation Agent | Task 3.0 | `classification.json` with confidence scores | Trust Matrix Notes, PRD §7 (F1.1) |
| 3.2 | Normalize payload into schema (`artifact_id`, `summary`, `confidence`, etc.) | Automation Agent | Task 3.1 | `normalized/<artifact_id>.json` matching sample schema | PRD §7 (Sample Schema) |
| 3.3 | Apply immutability guard (hash + write-once copy to `archive/`) | Automation Agent | Task 3.2 | Hash log entry `hashes.csv` | PRD §7 (F1.3) |
| 4.0 | Strategist reviews normalization output; approves or requests re-run | Strategist Agent | Task 3.3 | Approval record appended to `ingestion_manifest.json` | PRD §7 (Gate 1) |
| 4.1 | If re-run needed, automation agent regenerates normalization and re-hashes | Automation Agent | Task 4.0 (reject) | Updated normalized files + hash log | PRD §17 (Rollback) |
| 5.0 | Run trust dimension extraction (accuracy, bias, consistency, etc.) on normalized payload | Research Agent | Task 3.2 | `trust_dimensions/<artifact_id>.json` | Trust Matrix Notes, Model-Consensus Note |
| 5.1 | Cross-reference independent sources cited in payload; flag gaps | Research Agent | Task 5.0 | `trust_dimensions/<artifact_id>_gaps.md` | Trust Score Notes |
| 5.2 | Update centralized trust score ledger with latest model scores | Research Agent | Task 5.0 | `NOTES/trust_score_ledger.jsonl` | AI Model Trust Score Evaluation Report |
| 6.0 | Strategist updates routing rules in `PROMPTS/evergreen-app-prompts.json` for new artifact types | Strategist Agent | Tasks 5.0-5.2 | Modified prompt mappings with version tag | PRD §7 (F2.1-F2.3) |
| 6.1 | Commit change log entry in `ORCHESTRATION_LOGS/decision_trees/vX.json` | Strategist Agent | Task 6.0 | Updated decision tree JSON | PRD §18 |
| 7.0 | Generate orchestration brief for each artifact (objectives, dependencies, expected outputs) | Strategist Agent | Tasks 3.2, 6.0 | `briefs/<artifact_id>_brief.md` | PRD §7 (F2.3) |
| 7.1 | Produce meta-prompt packets tailored to assigned agents (Claude, GPT, etc.) | Strategist Agent | Task 7.0 | `handoffs/<agent>/<artifact_id>_prompt.json` | PRD §7 (F2.2), Agent Role Matrix |
| 8.0 | User validates trust score changes align with leadership priorities (e.g., AHP weighting) | User Action | Tasks 5.2, 6.0 | User-signed note `NOTES/trust_weighting_ack.md` | Trust Matrix Notes (Next Step Suggestion) |
| 9.0 | Execution agents consume prompts and generate outputs (code/docs/tests) | Execution Agents | Task 7.1 | Output artifacts in `outputs/<artifact_id>/` | PRD §7 (Plan Execution) |
| 9.1 | QC agents run checklist (`validation/<artifact_id>_qc.md`) achieving ≥95% pass rate | QC Agent | Task 9.0 | QC report with pass/fail and remediation items | PRD §7 (F4.1-F4.4), §17 Gate 2 |
| 9.2 | If failure, execution agents remediate and resubmit until pass threshold met | Execution Agents | Task 9.1 (fail) | Updated deliverables + QC addendum | PRD §17 (Rollback Protocol) |
| 10.0 | Continuity agent packages session bundle (status, diffs, next actions) | Continuity Agent | Tasks 7.1, 9.1 | `ORCHESTRATION_LOGS/SESSION_<timestamp>/continuity_bundle.zip` | PRD §7 (F5.1-F5.3), §16 |
| 10.1 | Telemetry agent publishes KPI snapshot to strategist channel | Automation Agent | Task 10.0 | KPI message (cycle time, coverage, validation rate) | PRD §10 step 8, KPI metrics |
| 11.0 | Strategist reviews telemetry; logs go/no-go decision using checklist | Strategist Agent | Task 10.1 | `go_nogo/SESSION_<timestamp>.md` with signed status | PRD §19 |
| 11.1 | User acknowledges go/no-go decision and approves release if "go" | User Action | Task 11.0 | User approval note appended to go/no-go file | PRD §17 Gate 3 |
| 12.0 | Archive session (normalized payloads, outputs, QC reports, telemetry) | Automation Agent | Task 11.1 | `archive/SESSION_<timestamp>/` complete snapshot | PRD §18 |
| 12.1 | Trigger retrospective template population (lessons, KPI deltas) | Strategist Agent | Task 12.0 | `RETROS/SESSION_<timestamp>.md` draft | PRD §16 (Retrospective & KPI Dashboard) |
| 12.2 | User schedules leadership review for trust model adjustments | User Action | Task 12.1 | Calendar event + meeting agenda | Model-Consensus Note (Feedback Loop) |
| 13.0 | Update README (or continuity doc) with any structural changes introduced | Strategist Agent | Task 6.0 & 12.0 | README section update + change log entry | PRD §18, README Maintenance |
| 13.1 | Version bump automation scripts (`nblm-integration-vX.Y` tag) | Automation Agent | Task 12.0 | Git tag + release notes | PRD §18 |
| 14.0 | Monitor telemetry heartbeat; alert strategist if no update within SLA | Automation Agent | Task 10.1 | Alert ticket in `ORCHESTRATION_LOGS/alerts/` | PRD §13 (Telemetry Risk) |
| 14.1 | User rotates credentials if telemetry alert indicates security issue | User Action | Task 14.0 (security alert) | Credential rotation confirmation in `_REFERENCE/` | PRD §12, Security Notes |

**Legend:**
- **Owner**: "User Action" denotes steps the human user (Rob) must perform. Other roles align with Agent Role Matrix.
- **Dependencies**: Task IDs that must complete (or fail) before current task starts.
- **Source Notes**: Primary note or PRD section informing the task.

---

## Supplemental Checklists
- **Model Trust Refresh:** Repeat Tasks 5.0–5.2 quarterly or upon major model update announcements (`NOTES/AI Model Trust Score Evaluation Report.md`).
- **NotebookLM Workflow:** Align Tasks 2.0–3.2 with NotebookLM export cadence to maintain continuous ingestion.
- **Leadership Brief Prep:** Combine outputs from Tasks 10.0, 12.1, and 12.2 to generate executive-ready updates.
