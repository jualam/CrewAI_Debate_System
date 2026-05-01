# CrewAI Debate System

CrewAI Debate System is a lightweight multi-agent application that simulates a structured debate around a given motion. It uses CrewAI to coordinate a debater agent that presents arguments for and against the motion, followed by a judge agent that evaluates both sides and delivers a verdict.

## Features

- Multi-agent debate workflow built with CrewAI
- Sequential execution of proposal, opposition, and judging tasks
- YAML-based configuration for agents and tasks
- LLM-generated arguments using `openai/gpt-4o-mini`
- Markdown outputs for each debate stage

## Project Structure

```text
crewai_debate_system/
|-- knowledge/                 # Optional project knowledge files
|-- output/                    # Generated debate outputs
|-- src/crewai_debate_system/
|   |-- config/
|   |   |-- agents.yaml        # Agent roles, goals, and models
|   |   `-- tasks.yaml         # Debate task definitions
|   |-- crew.py                # CrewAI agents, tasks, and workflow
|   `-- main.py                # Application entry point
|-- pyproject.toml
|-- requirements.txt
`-- README.md
```

## How It Works

The workflow runs three tasks in sequence:

1. The debater argues in favor of the motion.
2. The debater argues against the motion.
3. The judge reviews both arguments and selects the more convincing side.

Each task writes its result to the `output/` directory:

- `output/propose.md`
- `output/oppose.md`
- `output/decide.md`

## Requirements

- Python 3.10 or newer
- OpenAI API key
- CrewAI and project dependencies from `requirements.txt`

## Setup

Clone the repository and install the dependencies:

```bash
git clone https://github.com/jualam/CrewAI_Debate_System.git
cd CrewAI_Debate_System
pip install -r requirements.txt
```

Create a `.env` file in the project root and add your API configuration:

```env
OPENAI_API_KEY=your_openai_api_key
MODEL=gpt-4o-mini
```

## Usage

Run the debate workflow with:

```bash
crewai run
```

By default, the motion is defined in `src/crewai_debate_system/main.py`:

```python
inputs = {
    "motion": "There needs to be strict laws to regulate LLMs",
}
```

Update the `motion` value to run the debate on a different topic.

## Configuration

Agent behavior is managed in `src/crewai_debate_system/config/agents.yaml`, while task instructions and output files are managed in `src/crewai_debate_system/config/tasks.yaml`.

The main CrewAI workflow is defined in `src/crewai_debate_system/crew.py`, where agents and tasks are registered and executed using `Process.sequential`.
