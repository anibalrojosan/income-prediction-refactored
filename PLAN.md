# Project Transformation Prompt: From Prototype to Production-Ready (2026 Standards)

Use this prompt to guide an AI agent in transforming a personal project into a professional, recruiter-ready portfolio piece following the 2026 MLOps/Software Engineering stack.

---

## 1. The Goal
Transform a basic functional prototype into an industrialized system by focusing on:
- **Industrialized Focus:** Instead of forcing specific tools, engage in a collaborative dialogue to define the best stack for the project's specific domain (e.g., choosing between FastAPI vs. Django, or MLflow vs. Weights & Biases).
- **Modern Tooling Selection:** Discuss high-performance options (like `uv`, `Ruff`, `MyPy`) and their benefits for the specific use case.
- **Observability Strategy:** Define what to monitor (Drift, Latency, Accuracy) and which tools fit the scale (Evidently AI, Prometheus, ELK).
- **Lifecycle & AI Trends:** Explore if it's necessary implement them  Lifecycle Management (MLflow, DVC) and 2026 trends like Agentic Workflows or Trustworthy AI based on the project's complexity or it's better to focus in other áreas, not only the last trends.

---

## 2. Step-by-Step Execution Instructions

### Step 1: Codebase Assessment
- Analyze the current project structure and identify technical debt.
- Detect "Red Flags" (e.g., overfitting, lack of validation, manual deployment, spaguetti code, etc).
- **Narrative Shift:** Turn limitations into engineering opportunities (e.g., "Overfitting is an excuse to build robust monitoring", This is a oportunity to implement SOLID principles and Good software eng practices").

### Step 2: Strategic Planning (The ROADMAP)
Create a `doc/ROADMAP.md` file using a proggresion divided in phases as discused with the user

**Format:** Use a Tech Stack table followed by Phase-specific goals and requirements.

### Step 3: Task Breakdown (The GITHUB_PROJECTS)
Create a `github_projects.md` file in the root directory.
- Break each Phase into **Sprints**.
- Each Sprint must contain a detailed **Issue** format:
  - `Issue ID`, `Branch name`, `Type`, `Priority`.
  - `Description`: The "Why" and "What".
  - `Tasks`: Granular checkboxes including quality checks (`uv run ruff`).
  - `Acceptance Criteria`: Clear conditions for "Done".

### Step 4: Documentation of Progress (The DEVLOG)
Create a `doc/DEVLOG.md` file.
- Document daily achievements, challenges, and solutions.
- **Format:** `[YYYY-MM-DD]`, `Achievements`, `Challenges & Solutions`, `Next Steps`.

### Step 5: Infrastructure & Quality Gates
- Update `.gitignore` for modern Python/ML artifacts.
- Setup CI/CD logic (GitHub Actions) for automated Linting and Testing.

---

## 3. Reference File Formats

### ROADMAP.md Template
```markdown
# Technical Roadmap: [Project Name]
## Tech Stack
| Category | Tool | Purpose | Phase |
| --- | --- | --- | --- |
...
## Phase 1: [Name]
**Goal:** [Objective]
### Requirements
* [Task 1]
* [Task 2]
```

### GITHUB_PROJECTS.md Template
```markdown
### Sprint X: [Title]
**Issue:** `phaseX-0Y: [description]`
**Branch:** `feat/[branch-name]`
**Type:** [backend/ml/ops]
**Priority:** [High/Med/Low]
#### Tasks
- [ ] Task 1
- [ ] Task 2
#### Acceptance Criteria
- [ ] Condition 1
```

### DEVLOG.md Template
```markdown
[YYYY-MM-DD]
### [Topic]
#### Achievements
- ...
#### Challenges & Solutions
- **Challenge:** ...
- **Solution:** ...
#### Next Steps
- ...
```

---

## 4. Final Instruction to the Agent
"Act as a Senior ML/Software Engineer. Your mission is to guide me through this transformation. 

**CRITICAL:** Do not start by imposing a fixed stack. Instead:
1. **Analyze** my current code and identify its core purpose and limitations.
2. **Consult** with me: Start a dialogue to define the best '2026-ready' tools for *this specific project*. Discuss trade-offs (e.g., FastAPI vs. Django, or which Observability stack makes sense).
3. **Propose** the ROADMAP only after we have agreed on the strategic direction.
4. **Explain** the engineering decisions behind every choice to ensure it builds a strong narrative for recruiters."
