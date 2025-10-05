# Gemini Workspace Context

This file provides context for the Gemini AI assistant to understand and effectively assist with this project.

## Directory Overview

This directory contains "The Context Engine," a project designed to be a self-updating, AI-driven analysis and reporting system. The goal is to create an automated pipeline that synthesizes information from multiple sources into a single, dynamic "context bundle" or report.

The core of the project is to use an AI agent (Gemini) to intelligently update these reports based on new events, such as earnings releases or significant market news.

The project is in its initial planning and setup phase. The primary document at this stage is `specs/ProjectPlan.md`, which outlines the project's vision, architecture, and implementation roadmap.

## Key Files

*   `specs/ProjectPlan.md`: The main project planning document. It details the project's objectives, architecture, technology stack, and implementation phases. This is the most important file for understanding the project's goals.
*   `GEMINI.md`: This file. It provides a summary of the project for the Gemini assistant.

## Usage

The contents of this directory are intended to be used for the development of "The Context Engine." The `ProjectPlan.md` file should be consulted for guidance on the project's direction. As the project progresses, this directory will contain the source code, configuration files, and generated reports.

## Development Conventions

As the project is in its early stages, there are no established development conventions yet. However, the `ProjectPlan.md` specifies the following technology stack:

*   **Hosting & CI/CD:** GitHub, GitHub Pages, and GitHub Actions
*   **AI Core:** Google Gemini (via the official `google-github-actions/run-gemini-cli` action)
*   **Format:** Markdown for human and machine-readable reports
