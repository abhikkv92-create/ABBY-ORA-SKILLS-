# Abby ORA Skills - Claude Code Plugin Configuration

## Overview

This is the **Abby ORA Skills** plugin for Claude Code - an intelligent Oracle Fusion Cloud Expert System with memory, self-learning, and multi-agent orchestration.

**Version**: 2.0.0
**Type**: Claude Code Plugin (Uploadable)
**Mode**: STRICTLY OFFLINE - No external connections

---

## Plugin Architecture

### Directory Structure

```
ABBY-ORA-SKILLS-/
├── .claude-plugin/           # Plugin configuration
│   └── plugin.json          # Main plugin definition
├── skills/                   # Individual skill files (upload to Claude)
│   ├── abby-ora-master-skill.md    # Master skill with all domains
│   ├── scm-functional-consult/     # SCM functional expertise
│   ├── scm-planning-expert/        # Planning/ATP expertise
│   ├── api-integration-expert/    # API integration
│   ├── technical-architect/        # Architecture
│   ├── advanced-debugger/          # Troubleshooting
│   ├── qa-uat-expert/              # Testing
│   ├── workflow-orchestrator/      # Workflows
│   ├── industry-expert/           # Industry solutions
│   ├── pm-agent/                   # Project management
│   ├── research-scholar/          # Research
│   └── orchestrate-task/           # Multi-agent orchestration
├── agents/                   # Agent definitions (reference)
├── hooks/                   # Hook configurations
│   └── hooks.json          # Session hooks
├── memory/                  # Memory system
│   └── memory.json         # Memory configuration
├── processes/               # Process handlers
│   └── processes.json      # Workflow definitions
├── CLAUDE.md               # This file
└── README.md              # Documentation
```

---

## How to Use

### Option 1: Upload Master Skill (Recommended)

Upload `abby-ora-master-skill.md` to Claude. This single file provides:
- Complete Oracle Fusion Cloud expertise
- Intelligent memory tracking
- Automatic routing to specialist knowledge
- Self-learning capabilities
- Quality scoring

### Option 2: Upload Individual Skills

Upload specific skill files for focused expertise:
- `scm-functional-consult/` - SCM functional areas
- `scm-planning-expert/` - Planning & ATP
- `api-integration-expert/` - API integration
- `technical-architect/` - Architecture
- `advanced-debugger/` - Debugging
- `qa-uat-expert/` - Testing
- etc.

---

## Intelligent Features

### 1. Session Memory

The skill tracks conversation context across turns:
- Current domain (SCM/ERP/EPM/etc.)
- Active skill being used
- Query intent classification
- Complexity assessment
- Conversation history

### 2. Intent Classification

Automatically detects:
- **Domain**: SCM, ERP, EPM, HCM, CX, Technical
- **Intent**: functional, technical, troubleshooting, planning, qa, research
- **Complexity**: simple, medium, complex, expert

### 3. Intelligent Routing

Routes queries to appropriate specialists based on:
- Domain + intent classification
- Conversation context
- Task complexity

### 4. Quality Tracking

Scores responses on:
- Accuracy (correct Oracle guidance)
- Completeness (all aspects covered)
- Actionability (clear next steps)
- Safety (production considerations)

### 5. Self-Learning

Adapts based on successful interactions:
- Tracks successful response patterns
- Identifies improvement areas
- Updates contextual responses

---

## Configuration

### User Settings (via Claude)

| Setting | Default | Description |
|---------|---------|-------------|
| `memory_enabled` | true | Enable session memory |
| `audit_enabled` | true | Enable audit logging |
| `learning_mode` | adaptive | adaptive/conservative/strict |
| `response_verbosity` | standard | concise/standard/detailed |

---

## Supported Oracle Modules

| Module | Functional Areas |
|--------|------------------|
| **SCM** | Inventory, Order Management, Procurement, Manufacturing, Costing |
| **ERP** | Payables, Receivables, GL, Asset Management, Procurement |
| **EPM** | Planning, Budgeting, Consolidation, Financial Close |
| **HCM** | Human Capital Management |
| **CX** | Customer Experience |
| **Technical** | APIs, OIC, OCI, Security, Integration |

---

## Query Format

For best results, structure your query:

```
"I need help with [specific Oracle topic] for [specific scenario]"
```

Examples:
- "How do I set up ATP rules for a new item?"
- "Orders are stuck in processing - how to debug?"
- "What's the best approach for implementing Oracle Procurement?"

---

## Constraints

⚠️ **IMPORTANT CONSTRAINTS:**

1. **STRICTLY OFFLINE**: Does NOT connect to any external Oracle system
2. **NO API CALLS**: Does NOT make REST/SOAP calls to Oracle Fusion Cloud
3. **NO DATABASE**: Does NOT query Oracle databases directly
4. **KNOWLEDGE-BASED**: All guidance from Oracle documentation + implementation experience
5. **SAFE MODE**: Always recommends testing in non-production first
6. **ATTRIBUTION**: Contains permanent, unremovable attribution

---

## Plugin Components

### hooks.json
- Session start/end hooks for memory initialization
- Audit logging hooks for tracking
- Post-tool-use hooks for quality monitoring

### memory.json
- Session-based memory structure
- Intent classification rules
- Pattern recognition config
- Learning modes (adaptive/conservative/strict)

### processes.json
- Intent analysis process
- Agent routing rules
- Response synthesis workflow
- Quality evaluation metrics

---

## Attribution

**Developer**: Abhinav Verma
**Email**: Abbykkv@gmail.com
**Created**: April 24, 2026
**GitHub**: https://github.com/abhikkv92-create/ABBY-ORA-SKILLS-

---

*Upload the skill files to Claude and start getting expert Oracle Fusion Cloud guidance!*