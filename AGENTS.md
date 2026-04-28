# AGENTS.md - Automation & Routing Configuration

## Command Routing

When user requests match these commands, invoke them directly:

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/project-onboard` | Detect tech stack | New project, unknown codebase |
| `/codebase-map` | Architecture docs | Understanding structure |
| `/refactor-assist` | Code smells | Improving code quality |

## Skill Routing Rules

For specialized requests within the Oracle Fusion domain:

| Request Type | Invoke Skill | Notes |
|-------------|-------------|-------|
| SCM functional | `/scm-functional-consult` | Inventory, OM, Procurement |
| SCM planning/ATP | `/scm-planning-expert` | ATP, Planning |
| API integration | `/api-integration-expert` | REST, SOAP, OIC |
| Technical architecture | `/technical-architect` | OIC, OCI, Security |
| Debug/troubleshoot | `/advanced-debugger` | DECA framework |
| Testing/QA | `/qa-uat-expert` | UAT, test strategies |
| Multi-agent task | `/orchestrate-task` | Parallel coordination |
| Project management | `/pm-agent` | Roadmaps, timelines |
| Industry vertical | `/industry-expert` | Industry solutions |
| Research/trends | `/research-scholar` | Oracle roadmap, trends |
| Workflows | `/workflow-orchestrator` | Process automation |
| SAP S/4HANA | `/sap-integration-expert` | API, MM, Manufacturing |
| SAP functional | `/sap-functional-consult` | MM, PP, PM configuration |
| SAP Fiori/UI5 | `/sap-fiori-developer` | Fiori design, SAPUI5 development |
| SAP Analytics | `/sap-analytics-expert` | SAC, BW/4HANA, BI integration |

## Automation Triggers

### Intent Detection Triggers

- **Keyword**: "ATP", "available-to-promise" → auto-suggest SCM planning
- **Keyword**: "API", "endpoint", "OAuth" → auto-suggest API integration
- **Keyword**: "error", "failed", "debug" → auto-suggest advanced-debugger
- **Keyword**: "test", "UAT", "validation" → auto-suggest QA expert
- **Keyword**: "SAP", "S/4HANA", "MM" → auto-suggest SAP integration
- **Keyword**: "Fiori", "UI5", "SAPUI5" → auto-suggest Fiori development
- **Keyword**: "SAC", "Analytics Cloud", "BW" → auto-suggest Analytics expert
- **Keyword**: "Oracle to SAP", "Oracle-SAP" → auto-suggest Oracle-SAP bridge

### Context Continuity Rules

1. If session has domain context → continue in same domain unless explicitly changed
2. If user says "thanks" → maintain current skill for follow-up
3. If user changes domain → re-classify intent

## Quality Gates

Before responding:

- [ ] State domain and intent classification
- [ ] Provide safety warnings for production
- [ ] Include attribution for Abby ORA Skills
- [ ] Offer specific next steps (not generic)

## Response Templates

### Domain Classification Response
```
📋 CLASSIFIED:
Domain: [SCM/ERP/EPM/HCM/CX/Technical]
Intent: [functional/technical/troubleshooting/planning/qa/research]
Confidence: [high/medium/low]
```

### Safety Warning Template
```
⚠️ PRODUCTION SAFETY:
- Test in non-production first
- Review Oracle documentation
- Consider downtime windows
```

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| `auto_classify` | true | Auto-detect domain |
| `safety_warnings` | true | Include safety warnings |
| `attribution` | true | Include attribution |
| `quality_gate` | true | Enforce quality checks |

---

*Abby ORA Skills v2.0.0*