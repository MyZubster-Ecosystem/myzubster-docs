# MyZubster — App & Tool Roadmaps

This document defines how the tools already connected to the ChatGPT workflow are used across the project. It is an operating roadmap, not a claim that every integration is currently configured or automated.

## 1. ChatGPT — Orchestration & Intelligence

**Role:** central workspace for planning, analysis, drafting, technical reasoning, QA, and coordination.

### Roadmap
- Phase 1: project context, requirements, architecture notes
- Phase 2: technical analysis, documentation, diagrams, roadmap generation
- Phase 3: QA and consistency checks across project artifacts
- Phase 4: coordinate external tools and keep outputs linked
- Phase 5: maintain reusable project operating procedures

**Primary output:** decisions, specifications, prompts, documentation, reviews, and coordinated actions.

## 2. Slack — Team Communication & Execution

**Role:** operational communication, decisions, updates, review threads, and project coordination.

### Roadmap
- Phase 1: identify project channels and communication owners
- Phase 2: centralize architecture, roadmap, release, and design discussions
- Phase 3: use threads for decisions and follow-ups
- Phase 4: maintain lightweight project canvases for durable summaries
- Phase 5: connect milestones and release communication to the project documentation

**Primary output:** decisions and team-visible execution context.

## 3. GitHub — Source of Truth

**Role:** code, technical documentation, issues, pull requests, architecture references, and version history.

### Roadmap
- Phase 1: repository structure and documentation index
- Phase 2: architecture and security documentation
- Phase 3: roadmap and visual-production documentation
- Phase 4: implementation tracking through issues/PRs
- Phase 5: release and production-readiness evidence

**Primary output:** versioned source and project documentation.

## 4. Canva — Visual Production

**Role:** editable source for social graphics, technical diagrams, roadmap screens, and visual communication.

### Roadmap
- Phase 1: visual foundation / design language
- Phase 2: five core product explainers
- Phase 3: technical architecture diagrams
- Phase 4: seven roadmap screens
- Phase 5: channel adaptations
- Phase 6: visual QA and final asset library

**Primary output:** editable visual assets and reusable design system.

## 5. Cross-App Operating Flow

```text
CHATGPT
  │  plan / analyze / specify
  ▼
GITHUB ◄────────────► SLACK
  │                    │
  │ source of truth    │ communication / decisions
  │                    │
  └──────────┬─────────┘
             ▼
           CANVA
             │
             │ visual assets
             ▼
       SOCIAL / DOCS / WEB
```

## Working principle

Use each tool for its strongest role rather than duplicating the source of truth:

- **ChatGPT:** reasoning and orchestration
- **GitHub:** versioned source and durable technical documentation
- **Slack:** communication and operational coordination
- **Canva:** editable visual source files

When a claim depends on the actual implementation, validate it against the current repository before publishing it as a production fact.

## Current status

- ChatGPT workflow: active
- GitHub documentation: active
- Slack workflow: available for coordination
- Canva visual production: active where quota permits; some new visual generation is currently quota-limited
