<!--
Sync Impact Report:
- Version change: 1.2.0 -> 1.2.1
- Modified principles: None
- Templates requiring updates: None
- Follow-up TODOs: None
-->
# The Context Engine Constitution

## Core Principles

### I. AI-First Analysis
The core logic of the system relies on an AI agent (Google Gemini) to perform analysis and generate reports. All data processing and synthesis should be designed to leverage the AI's capabilities.

### II. Automation by Default
The system is designed as an event-driven, automated pipeline. Manual interventions should be the exception, not the rule. All processes should be defined as code within the CI/CD framework.

### III. Versioned, Living Documents
All reports are "living documents" that are continuously updated. Every change is tracked through Git, providing a complete version history.

### IV. Markdown for Readability
Reports are authored in Markdown to ensure they are both human-readable and machine-parsable. This facilitates consumption by both people and other automated systems.

### V. GitHub-Native Ecosystem
The project is built entirely on the GitHub platform, using GitHub Actions for CI/CD, GitHub Pages for hosting, and the repository for all configuration and data.

### VI. Data Lineage & Provenance
All external data sources must be explicitly logged, including what data was fetched, its source URL or identifier, the timestamp, and the method of retrieval.

### VII. Fail-Safe & Transparency
When automation fails, the system must degrade gracefully. This includes mechanisms for human review of failures and publicly visible error logs to ensure transparency.

### VIII. Minimalism
Complexity is the enemy. All added features, tools, or dependencies must be strictly justified against their long-term maintenance costs.

### IX. Data-as-Code (DAC)
All data, including configurations, targets, and initial report templates, are treated as code. They are stored in version-controlled text files (e.g., `.txt`, `.md`, `.yml`) to ensure traceability, reviewability, and to enable automated, repeatable processes.

## Governance

All pull requests and reviews must verify compliance with these principles. Complexity or deviation from these principles must be justified.

**Version**: 1.2.1 | **Ratified**: 2025-10-05 | **Last Amended**: 2025-10-05