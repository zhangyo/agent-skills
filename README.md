# agent-skills

  A public library of agent skills: reusable, file-based workflows and prompts that standardize complex engineering tasks across Codex and other agent runtimes.

  ## What’s inside
  Each skill lives in its own folder and includes a `SKILL.md` that defines the workflow, inputs, and outputs. Some skills include `assets/` for templates or references.

  ## Usage
  1) Copy a skill folder into your agent’s skills directory.
  2) Follow the instructions inside the skill’s `SKILL.md`.
  3) Keep task artifacts (plans, status, checklists) in your repo as defined by the skill.

  ## Example
  - `ralf-loop`: file-driven loop for iterative work using prompt/instructions/checklist/status artifacts.

  ## Contributing
  PRs are welcome. Please:
  - Keep skills self-contained.
  - Use ASCII unless the project requires Unicode.
  - Document inputs/outputs and any required tools.
  - Include templates under `assets/` if the skill references them.

  ## License
  MIT
