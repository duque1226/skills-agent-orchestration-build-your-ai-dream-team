# Agent team

For Mona's Project Pulse dashboard, I will use a custom four-agent team defined in the repository under `.github/agents/` and orchestrated through GitHub Copilot CLI inside a Codespace.

- Planner — Model: Claude Opus 4.7 (copilot). Responsible for researching the codebase, identifying requirements and edge cases, and producing an implementation plan with file ownership and dependencies. Definition: `.github/agents/planner.agent.md`
- Orchestrator — Model: Claude Opus 4.7 (copilot). Responsible for breaking the work into phases, delegating tasks to specialist agents, coordinating execution, and verifying that the integrated dashboard hangs together. Definition: `.github/agents/orchestrator.agent.md`
- Designer — Model: Gemini 3.1 Pro (copilot). Responsible for the dashboard's UX, information architecture, accessibility, visual styling, and Project Pulse-specific interaction and layout decisions. Definition: `.github/agents/designer.agent.md`
- Coder — Model: GPT-5.5 (copilot). Responsible for implementing the actual application logic, bug fixes, and any assigned runnable app support needed for the dashboard in the approved file scope. Definition: `.github/agents/coder.agent.md`

This team is designed to work in sequence and in parallel where file ownership does not overlap: the Planner proposes the roadmap, the Orchestrator coordinates execution, the Designer shapes the front-end experience, and the Coder delivers the build. GitHub Copilot CLI in a Codespace is the orchestration layer that manages the workflow and delegates to these specialized agents.
