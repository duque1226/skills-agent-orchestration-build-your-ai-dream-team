# Project Pulse dashboard implementation plan

## Goal

Build a lightweight static Project Pulse dashboard for Mona's team using GitHub Copilot CLI in a Codespace. The final experience should help contributors quickly understand which projects are active, who owns them, their statuses, recent activity, priority, and a short contributor-friendly summary.

The dashboard will live in a small static app with these files:

- `app/index.html`
- `app/styles.css`
- `app/project-data.json`
- `.vscode/launch.json`

This plan is intended to be orchestrated by the Planner and executed by the Designer and Coder under the Orchestrator's coordination.

## Implementation phases

### Phase 1: Define the data and dashboard structure

- Planner: confirm the data model and the UI requirements based on the Project Pulse brief.
- Owner: `app/project-data.json`
- Scope:
  - Create a top-level `projects` array.
  - Define each project record with `name`, `owner`, `status`, `recentActivity`, and `priority`.
  - Keep the structure consistent with the static app that will render cards and badges.
- Dependencies:
  - The UI layout and card templates depend on the data keys and values being stable.
  - The Coder can start this file before the Designer finalizes the exact visual styling, because the content model is independent from rendering polish.

### Phase 2: Create the dashboard shell and semantic markup

- Owner: `app/index.html`
- Scope:
  - Add a clear Project Pulse heading and page-level dashboard structure.
  - Include a list or grid of project cards that can render from JSON data.
  - Provide accessible semantics for headings, labels, and descriptive text.
  - Keep the page lightweight and focused on readability and contributor clarity.
- Dependencies:
  - This file must align with the project data schema from `app/project-data.json`.
  - It should reference the stylesheet and the data source in a way that works when opened from a browser via a local launch configuration.

### Phase 3: Apply the dashboard visual design

- Designer responsibility: shape the experience and visual system.
- Owner: `app/styles.css`
- Scope:
  - Create a polished dashboard look rather than a plain document.
  - Use project cards, status badges, readable spacing, contrast, and hierarchy.
  - Add responsive layout rules so the dashboard reads well across widths.
  - Define deterministic CSS hooks such as `.dashboard`, `.project-card`, and status classes.
- Dependencies:
  - The design is informed by the HTML structure established in `app/index.html`.
  - It also depends on the data categories and labels defined in `app/project-data.json` so badges and labels are consistent with actual values.

### Phase 4: Add the run configuration

- Owner: `.vscode/launch.json`
- Scope:
  - Create a launch configuration named `Run Project Pulse Dashboard`.
  - Set the working directory to the `app/` folder.
  - Launch the app so the browser opens `index.html` instead of a directory listing.
  - Keep the configuration deterministic and easy for a learner to run.
- Dependencies:
  - This should be created after the app structure and file references are stable.
  - It depends on the final output path conventions used by `app/index.html` and the static app layout.

## Designer and Coder responsibilities

### Designer

The Designer is responsible for:

- information hierarchy and visual clarity
- accessibility and readable contrast
- project cards, status badge design, spacing, and typography
- dashboard flow that makes priorities and activity obvious at a glance
- ensuring the first impression looks like a real Project Pulse dashboard rather than a bare HTML mockup

The Designer works primarily on `app/index.html` and `app/styles.css`, following the brief and ensuring the user experience is contributor-friendly.

### Coder

The Coder is responsible for:

- implementing the static UI structure and app wiring
- creating and validating the JSON data format
- ensuring the HTML references the correct CSS and data files
- creating the launch configuration for local preview in VS Code
- verifying that the dashboard loads correctly and that all referenced files exist in the expected locations

The Coder owns the implementation work in `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`, with design guidance from the Designer when the styling is being finalized.

## Dependencies

- `app/project-data.json` must exist before the HTML can render the dashboard data reliably.
- `app/index.html` depends on the final data keys and project card structure defined in `app/project-data.json`.
- `app/styles.css` depends on the final semantic structure from `app/index.html`.
- `.vscode/launch.json` depends on the final app folder layout and the fact that the dashboard is served from `app/` and opens `index.html`.
- The Orchestrator should review these dependencies before approving parallel execution to avoid file overlap and inconsistent naming.

## Parallel work decisions

The work can be split as follows:

- Parallelizable after the data model is agreed:
  - The Designer can begin styling in `app/styles.css` based on the planned HTML structure while the Coder prepares `app/project-data.json`.
  - The Coder can work on the HTML shell and the data file at the same time if the contract for field names is already clear.
- Not parallelizable without coordination:
  - The final CSS and markup must align on structure and class names.
  - The launch configuration should only be finalized after the dashboard files are stable and the browser entry path is confirmed.
- Recommended orchestration flow:
  1. Planner defines the data contract and phase plan.
  2. Coder produces the data and HTML shell.
  3. Designer refines the styling to match the structure.
  4. Coder finalizes the launch configuration and verifies the preview opens correctly.

## Validation expectations

The implementation is considered complete when the following are true:

- `app/index.html` renders a clear Project Pulse dashboard with a title and project cards.
- `app/styles.css` provides a polished visual layout with readable spacing, badges, and contrast.
- `app/project-data.json` contains a valid top-level `projects` array with the required fields.
- `.vscode/launch.json` exists with a configuration named `Run Project Pulse Dashboard` and opens `index.html` from the `app/` directory.
- The dashboard loads successfully without a directory listing, showing the actual Project Pulse UI instead of the filesystem.
- The page communicates status, owner, recent activity, and priority clearly enough for contributors to scan quickly.

## Outcome

This plan ensures the dashboard is built in a structured, low-risk sequence: define the data model, build the shell, refine the design, and validate the browser launch. The Orchestrator coordinates the work, the Planner keeps the phases clear, the Designer shapes the experience, and the Coder turns the plan into a runnable, validated dashboard.
