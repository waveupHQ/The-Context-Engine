# **Project Plan: The Context Engine**

**A Self-Updating, AI-Driven Analysis & Reporting System**

## **1\. Executive Summary**

**The Problem:** Financial analysis platforms like Simply Wall St provide excellent data visualization but often suffer from model inaccuracies and data lag. Relying on a single, automated source can be misleading. A multi-tool, human-in-the-loop approach is superior but difficult to maintain and scale.

**The Solution:** "The Context Engine" is a project to build an automated system that synthesizes information from multiple best-in-class sources into a single, dynamic "context bundle" or report. It leverages an AI agent (Google's Gemini) to intelligently update these reports based on new events, such as earnings releases or significant market news.

**Core Objective:** To create a living, version-controlled analysis report for any given asset (starting with stocks), which can be consumed by both humans for quick insights and other AI agents for deeper, programmatic analysis.

**Technology Stack:**

* **Hosting & CI/CD:** GitHub, GitHub Pages, and GitHub Actions  
* **AI Core:** Google Gemini (via the official google-github-actions/run-gemini-cli action)  
* **Format:** Markdown for human and machine-readable reports

## **2\. System Architecture**

### **High-Level Overview**

The system operates as an automated, event-driven pipeline entirely within the GitHub ecosystem. On a recurring schedule or manual trigger, a GitHub Action workflow executes the following steps for each target asset:

1. **Fetch New Data:** Gathers the latest news or data points from external sources.  
2. **Prepare Context:** Reads the existing Markdown report for the asset.  
3. **Construct Prompt:** Combines the new data and the existing report into a carefully engineered prompt using a predefined template.  
4. **Invoke AI Agent:** Sends the prompt to the Gemini model, which analyzes the information and generates a complete, updated version of the report.  
5. **Publish:** Commits the updated report back to the repository, which is then automatically published as a static webpage via GitHub Pages.

### **Architectural Diagram**

This diagram illustrates the flow of information and processes within the system.

graph TD  
    subgraph GitHub Repository  
        A\["src/ (Prompts, Templates, Targets)"\] \-- "Provides input" \--\> B  
        B((".github/workflows/analyzer.yml")) \-- "Orchestrates" \--\> C & D  
    end

    subgraph External World  
        E\[News/Data APIs\]  
    end

    subgraph GitHub Actions Runner  
        C\["Step 1: Fetch News (curl)"\]  
        D\["Step 2: Prepare Prompt"\]  
        F\["Step 3: Invoke Gemini CLI Action"\]  
        G\["Step 4: Generate Updated Report"\]  
    end

    subgraph Published Output  
        I\["docs/ (GitHub Pages Website)"\]  
    end

    E \-- "Provides new data" \--\> C  
    A \--\> D  
    D \-- "Sends final prompt" \--\> F  
    F \-- "Returns Markdown text" \--\> G  
    G \-- "Writes to file" \--\> H(Updated .md file)  
    B \-- "Triggers" \--\> C  
    H \-- "Commits back to repo" \--\> I

### **Component Deep-Dive**

* **src/ (The Engine's Configuration):** This is the heart of the system's logic. It is modularized by report type (e.g., stock\_analysis). Each module contains:  
  * **prompts/**: Stores the master text prompts that instruct the Gemini agent on its role, rules, and task.  
  * **templates/**: Holds the skeletal Markdown structure for creating new, empty reports.  
  * **targets.txt**: A simple text file listing the assets to analyze (e.g., AAPL, GOOGL), making it easy to add or remove targets.  
* **.github/workflows/ (The Automation Layer):** This directory contains the YAML files that define the CI/CD pipeline using GitHub Actions. The workflow is responsible for scheduling the job, checking out the code, managing secrets (like the API key), orchestrating the steps, and committing the results.  
* **Gemini CLI Action (The Intelligence Core):** We use the official google-github-actions/run-gemini-cli action. This is the "brain" of the operation. It receives the final, context-rich prompt and leverages the power of the Gemini model to perform the analytical and regenerative task of updating the report.  
* **docs/ (The Publication Layer):** This directory is configured as the root for GitHub Pages. Any Markdown files committed here are automatically rendered and served as a static website. This folder contains the final, user-facing output—the "context bundles."

## **3\. Folder Structure**

The project uses a modular folder structure designed for scalability and maintainability.

The-Context-Engine/  
│  
├── .github/  
│   └── workflows/  
│       └── stock\_analyzer.yml  
│  
├── docs/  
│   ├── index.md  
│   ├── stocks/  
│   │   ├── AAPL.md  
│   │   └── GOOGL.md  
│   └── crypto/  
│  
├── src/  
│   └── stock\_analysis/  
│       ├── prompts/  
│       │   └── update\_report.txt  
│       ├── templates/  
│       │   └── report\_template.md  
│       └── targets.txt  
│  
└── README.md

## **4\. Implementation Roadmap**

The project will be built in four distinct phases:

* **Phase 1: The Foundation (Manual v0)**  
  * Set up the GitHub repository and folder structure.  
  * Enable GitHub Pages on the docs/ directory.  
  * Manually create the first complete, high-quality stock report for a single ticker (e.g., AAPL.md) to serve as a gold-standard template.  
* **Phase 2: The Automation Engine**  
  * Create the initial stock\_analyzer.yml GitHub Action workflow.  
  * Implement schedule and workflow\_dispatch triggers.  
  * Add the final git commit steps to save changes, but leave the core AI logic as a placeholder.  
* **Phase 3: The Intelligence Integration**  
  * Secure the GOOGLE\_API\_KEY as a GitHub secret.  
  * Finalize the prompt in src/stock\_analysis/prompts/update\_report.txt.  
  * Integrate the google-github-actions/run-gemini-cli action into the workflow, dynamically building the prompt from the templates and fetched news.  
* **Phase 4: Scaling & Expansion**  
  * Modify the workflow script to loop through all tickers listed in targets.txt.  
  * Refine the news-fetching mechanism to be more robust.  
  * Begin planning for the next report type (e.g., Crypto) by creating a new module in the src/ directory.