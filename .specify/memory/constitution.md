<!--
<Sync Impact Report>
Version change: 1.0.0 (old) → 1.1.0 (new)
List of modified principles/sections:
  - Principle I. Spec-Driven First (Non-Negotiable)
  - Principle II. AI-Assisted but Human-Governed
  - Principle III. Education-First, Tool-Second
  - Principle IV. Physical-World Grounding
  - Principle V. Progressive Complexity
  - Principle VI. Reproducibility & Hands-On Bias
  - Principle VII. Long-Term Relevance
  - Technical & Structural Constraints
  - Development & Writing Workflow
  - Governance
Added sections: None (existing template sections filled)
Removed sections: None
Templates requiring updates:
  - .specify/templates/plan-template.md: ⚠ pending (Constitution Check section needs definition)
  - .specify/templates/spec-template.md: ⚠ pending (Indirect influence of principles on spec writing)
  - .specify/templates/tasks-template.md: ⚠ pending (Indirect influence of principles on task breakdown)
  - .gemini/commands/*.toml: ✅ updated (No changes needed)
Follow-up TODOs: None
</Sync Impact Report>
-->
# Physical AI & Humanoid Robotics Textbook Constitution
<!-- Spec-Driven Book Constitution for Physical AI & Humanoid Robotics -->

## Core Principles

### I. Spec-Driven First (Non-Negotiable)
All book content must be driven by written specifications.  
Every chapter, section, diagram, exercise, and project must have a defined specification before any content is generated.  
No ad-hoc or free-form writing is allowed.

Specifications must clearly define:
- Learning objectives
- Scope and exclusions
- Expected outputs
- Review and acceptance criteria
Specifications must be created by Subject Matter Experts (SMEs) or designated authors and formally approved by a lead author or editorial board before content generation begins.

### II. AI-Assisted but Human-Governed
The book is generated using AI via **geminiCLI**, but final authority always rests with human reviewers.  
AI output must never be accepted blindly.

AI acts as a co-author, not a decision-maker.  
All generated content must be reviewed for:
- Accuracy
- Pedagogical clarity
- Alignment with course goals
Human review is mandatory at key milestones: after initial generation of each major section/chapter, prior to integration into the Docusaurus framework, and before final publication. Continuous spot-checks are encouraged.

### III. Education-First, Tool-Second
Learning outcomes take priority over tools and technologies.  
Technologies such as ROS 2, Gazebo, Unity, or NVIDIA Isaac are introduced only when they provide clear educational value.

Each concept must follow this flow:
- Conceptual foundation
- Practical example
- Real-world application

Tool complexity must never obscure understanding. A tool provides "clear educational value" if it (a) directly illustrates a core concept, (b) enables hands-on experimentation, and (c) does not introduce excessive setup burden disproportionate to learning gains.

### IV. Physical-World Grounding
This textbook focuses on **Physical AI**, not purely abstract or digital AI.

All major topics must address:
- Real-world physical constraints
- Sensors and actuators
- Noise, latency, and uncertainty
- Safety and failure modes

Idealized or unrealistic assumptions are not permitted. Examples include: perfectly reliable sensors, instantaneous communication, infinite computational power, or absence of friction/gravity where physically relevant.

### V. Progressive Complexity
Content must follow a beginner-to-advanced progression.

Rules:
- Start with fundamentals
- Increase complexity incrementally
- Each chapter builds on prior knowledge

Sudden abstraction jumps or unexplained complexity are prohibited. Peer review checklists and automated content analysis tools (if available) must actively flag sections introducing more than two new, complex concepts without prior scaffolding or explicit definition within a single page.

### VI. Reproducibility & Hands-On Bias
All practical content must be reproducible.

Each hands-on section must include:
- Clear setup instructions
- Assumptions and constraints
- Expected results
- Specific versions of all required tools, libraries, and operating systems.

Readers must be able to build, simulate, test, and iterate independently. A dedicated `reproducibility.md` file must accompany each chapter detailing the validated environment.

### VII. Long-Term Relevance
The textbook must prioritize long-term foundational knowledge.

Guidelines:
- Avoid short-lived hype
- Emphasize core principles
- Design content to be extensible and updatable

The goal is relevance over years, not trends. Content will prioritize principles, fundamental algorithms, and established best practices. Technologies will be evaluated for inclusion based on their widespread adoption, industry impact, and projected longevity (e.g., actively maintained open-source projects, established industry standards).

## Technical & Structural Constraints

- Mandatory Stack (Target Versions for 2025 Q4)
  - geminiCLI (AI-assisted content generation - Latest Stable)
  - Spec-Kit Plus (specification management - Latest Stable)
  - Docusaurus (documentation and textbook framework - v3.x LTS)
  - GitHub Pages (deployment)

- Markdown-first content
- Single unified repository
- Clear separation between specifications and generated content
- No proprietary tools without explicit justification

## Development & Writing Workflow

1. Define a master book specification
2. Create chapter-level specifications
3. Validate specifications against this Constitution
4. Generate initial content drafts using geminiCLI, guided by the chapter-level specifications and adhering to established tone/style guidelines.
5. Perform human review and refinement
6. Integrate content into Docusaurus
7. Iterate continuously with version control

Skipping or reordering steps is not allowed.

## Governance

This Constitution supersedes all other project documents and practices.

Rules:
- Any content or decision violating this Constitution is invalid
- Amendments to this Constitution require a formal proposal, rationale, a migration/impact analysis, and approval by a two-thirds majority of the editorial board. Approved amendments must be documented as Architectural Decision Records (ADRs).

All contributors are responsible for ensuring:
- Educational integrity
- Conceptual clarity
- Specification compliance

**Version**: 1.1.0 | **Ratified**: 2025-12-22 | **Last Amended**: 2025-12-22