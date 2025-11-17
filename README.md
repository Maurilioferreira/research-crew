## Research Crew

Small crew of two agents built with crewAI for topic research and markdown report generation.

### Crew.ai
Crew.ai is a framework for building multi-agent AI workflows: define specialized agents, orchestrate their tasks in sequences or hierarchies, and plug in tools (search, code exec, custom APIs) to produce end-to-end outputs with clear roles, goals, and shared context.
[crewAI](https://crewai.com)


### What it does
- Prompts you for a topic, researches it using a Brave search tool, and produces a markdown report (`report.md`).
- Agents: `researcher` finds 10 key points; `reporting_analyst` turns them into full sections.
- Tasks/config live in `research_crew/config/{agents,tasks}.yaml` and are interpolated with inputs (topic, current_year).
- Knowledge source example lives in `knowledge/user_preference.txt` and can be expanded with more files.

### Requirements
- Python 3.10–3.13
- Dependencies are in `pyproject.toml` (primarily `crewai[tools]>=0.130.0`).
- Brave Search access is required for `BraveSearchTool` (set the expected env vars per crewAI/tools docs, e.g., `BRAVE_API_KEY`).

### Install
```bash
pip install -e .
```

### Run
```bash
research_crew
# or
python -m research_crew.main
```
You will be prompted for a topic; the crew runs sequentially and writes `report.md`.

### Other entry points
- Training: `train <iterations> <output_file>` (uses topic `AI LLMs` as default input).
- Replay: `replay <task_id>`
- Test: `test <iterations> <eval_llm>` (uses topic `AI LLMs` as default input).
These map to functions in `research_crew/main.py` via the scripts defined in `pyproject.toml`.

### Customizing
- Update agent roles/goals/backstories in `research_crew/config/agents.yaml`.
- Adjust task descriptions/outputs in `research_crew/config/tasks.yaml`.
- Add tools under `research_crew/tools/` and attach them to agents in `research_crew/crew.py`.
- Add more knowledge files under `knowledge/` for retrieval support as needed.

