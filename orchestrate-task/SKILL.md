---
name: orchestrate-task
description: Orchestrate complex Oracle SCM tasks using the multi-agent AI system. Routes queries to specialized agents, synthesizes responses, and enables self-learning. Use for any multi-step or cross-module Oracle SCM query.
disable-model-invocation: false
---

================================================================================
DEVELOPED BY: ABHINAV VERMA | EMAIL: Abbykkv@gmail.com | CREATED: April 24, 2026
GitHub: https://github.com/abhikkv92-create/ABBY-ORA-SKILLS-
================================================================================

# Oracle SCM Multi-Agent Task Orchestrator

You are invoking the Master Orchestrator Agent (MOA) for the Oracle Fusion Cloud SCM AI ecosystem.

## How It Works

Given the user's task description ($ARGUMENTS), the orchestrator will:

1. **Classify Intent** — Determine if the query is FUNCTIONAL, TECHNICAL, QA, RESEARCH, or PLANNING
2. **Decompose Task** — Break complex queries into atomic sub-tasks
3. **Route to Agents** — Dispatch to the right specialized agent(s):
   - SCM module config/setup → `/oracle-scm-ai-agent:scm-functional-consult`
   - Demand planning, ATP, ASCP → `/oracle-scm-ai-agent:scm-planning-expert`
   - REST/SOAP API design → `/oracle-scm-ai-agent:api-integration-expert`
   - System architecture → `/oracle-scm-ai-agent:technical-architect`
   - Test scripts / UAT → `/oracle-scm-ai-agent:qa-uat-expert`
   - Error logs / stack traces → `/oracle-scm-ai-agent:advanced-debugger`
   - Industry best practices → `/oracle-scm-ai-agent:industry-expert`
   - Roadmaps / project timelines → `/oracle-scm-ai-agent:pm-agent`
   - Innovation / AI trends → `/oracle-scm-ai-agent:research-scholar`
   - Workflow / approval processes → `/oracle-scm-ai-agent:workflow-orchestrator`
4. **Synthesize** — Combine agent outputs into a coherent final response
5. **Evaluate Quality** — Score response and trigger feedback loop if needed

## Usage

Provide a natural language description of your Oracle SCM task:

```
/oracle-scm-ai-agent:orchestrate-task Why is ATP calculation wrong for Item XYZ in organization M1?
```

## Response Format

The orchestrator returns:
- **Intent Classification** — What type of query this is
- **Agents Engaged** — Which specialist agents were dispatched
- **Synthesized Answer** — Comprehensive response combining all agent outputs
- **Confidence Score** — Quality metric (0-1)
- **Action Items** — Concrete next steps
- **Sources** — Oracle docs, MOS notes, API references used