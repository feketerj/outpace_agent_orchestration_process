# Agent Orchestration Process — Baseline Repository

**Repository:** `https://github.com/feketerj/outpace_agent_orchestration_process`

**Purpose:** Comprehensive research, frameworks, and reusable resources for building autonomous AI agent-driven applications with emphasis on deterministic, modular, and safe orchestration patterns.

---

## Repository Structure

```
agent_orchestration_baseline/
├── README.md                                    # This file
├── _REFERENCE/                                  # Primary user context & configuration
│   ├── user_technical_execution_doc.md          # User preferences, philosophy, experience level
│   └── project_api_keys.md                      # API keys, subscriptions, GitHub token
│
├── RESEARCH/                                    # Frameworks, strategies, & findings
│   ├── frameworks/                              # Agent orchestration framework analysis
│   │   ├── agent-orchestration-best-practices.md
│   │   └── you_ai_agent_orchestration.md
│   ├── strategies/                              # Application building strategies
│   │   ├── agentic-application-build-strategies.md
│   │   └── agentic-nblm-integration-prd.md
│   └── open_source/                             # Open source library research
│       └── open-source-prompt-libraries.md
│
├── PROMPTS/                                     # Reusable LLM prompts & patterns
│   ├── evergreen-app-prompts.json               # Master prompt library (all roles/categories)
│   ├── by-provider/                             # Prompts organized by AI provider
│   │   ├── claude-prompts.txt
│   │   ├── gpt-prompts.txt
│   │   ├── gemini-prompts.txt
│   │   ├── mistral-prompts.txt
│   │   └── nous-prompts.txt
│   └── archive/                                 # Previous draft versions
│       ├── original-prompts-app-building.txt
│       ├── user-prompts-app-building-draft.txt
│       └── user-prompts-app-building-draft2.txt
│
├── NOTES/                                       # External research & comments
│   ├── perplexity-research-notes.txt
│   └── dr-prompt-agent-frameworks.txt
│
└── ARCHIVE/                                     # Superseded document variants
    └── [deprecated versions of reference docs]
```

---

## Quick Navigation

### For New Agents Starting a Session
1. **First:** Read `_REFERENCE/user_technical_execution_doc.md` to understand user preferences and project philosophy
2. **Context:** Review `_REFERENCE/project_api_keys.md` for GitHub token and API access
3. **Frameworks:** Check `RESEARCH/frameworks/` for orchestration patterns and best practices
4. **Prompts:** Use `PROMPTS/evergreen-app-prompts.json` as the master prompt library

### For AI Providers
- **Claude:** `PROMPTS/by-provider/claude-prompts.txt`
- **GPT:** `PROMPTS/by-provider/gpt-prompts.txt`
- **Gemini:** `PROMPTS/by-provider/gemini-prompts.txt`
- **Mistral:** `PROMPTS/by-provider/mistral-prompts.txt`
- **Nous:** `PROMPTS/by-provider/nous-prompts.txt`

### For Development References
- **Agent Orchestration Best Practices:** `RESEARCH/frameworks/agent-orchestration-best-practices.md`
- **Comprehensive Framework Analysis:** `RESEARCH/frameworks/you_ai_agent_orchestration.md`
- **Application Building Strategy:** `RESEARCH/strategies/agentic-application-build-strategies.md`
- **NBLM Integration PRD:** `RESEARCH/strategies/agentic-nblm-integration-prd.md`

---

## Key Principles

From `user_technical_execution_doc.md`:

✅ **Slow, safe, correct** — Prioritize accuracy and reliability over speed
✅ **Modular execution** — Break tasks into atomic, context-window-compliant units
✅ **>95% confidence threshold** — Execute autonomously only when highly confident
✅ **Clear handoff protocols** — Document state, dependencies, and next steps
✅ **Human oversight** — Include review gates for critical or high-risk tasks

---

## GitHub Integration

**Fine-grained Token Name:** `Repo_Clean_Up`
**Expires:** May 24, 2026
**Token Location:** `_REFERENCE/project_api_keys.md`

Local workspace and GitHub repository are mirrors — all structural changes should be committed and pushed to maintain sync.

---

## File Naming Conventions

- **Directories:** UPPERCASE (e.g., `_REFERENCE`, `RESEARCH`, `PROMPTS`)
- **Files:** kebab-case for clarity (e.g., `claude-prompts.txt`, `agent-orchestration-best-practices.md`)
- **Avoid:** underscores in file names, mixed case, or generic naming

---

## Maintenance

- **Active files** stay in primary directories
- **Previous versions** move to respective `archive/` folders
- **Superseded documents** move to root `ARCHIVE/` folder
- **Update this README** when adding new top-level categories

---

## Contact & Repository

**Owner:** Rob Fekete (rob@outpacesolutions.net)
**GitHub:** https://github.com/feketerj/outpace_agent_orchestration_process
**Created:** October 2025
