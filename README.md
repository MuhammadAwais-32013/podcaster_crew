# Podcaster Crew

## Project Overview

Podcaster Crew is a Python-based multi-agent AI application built with CrewAI that automates the research-to-podcast workflow. It uses specialized agents to gather information on a topic, turn that research into a well-structured markdown report, and generate a natural two-host podcast script. The project then uses Gemini Text-to-Speech to convert the final script into an audio file saved in the outputs folder.

This project is designed to help automate content creation for topics like AI trends, industry updates, research summaries, and podcast-ready storytelling with minimal manual effort.

## Capabilities

- Research any topic using an AI researcher agent
- Collect recent developments, articles, and important findings
- Organize findings into a detailed markdown report
- Convert the report into an engaging podcast script with two hosts
- Add natural dialogue, humor, pauses, and sound-effect style narration
- Generate podcast audio using Gemini voice synthesis
- Save generated outputs in the `outputs/` directory
- Customize agents, tasks, and topic inputs for different use cases
- Run locally with Python and CrewAI in a simple, repeatable workflow

## Why This Project?

Podcaster Crew demonstrates how multiple AI agents can collaborate in a real workflow:
1. Researcher gathers facts and trends
2. Reporting Analyst structures the findings
3. Scriptwriter turns the analysis into a podcast outline and dialogue
4. Voice generation creates final audio output

This makes it a practical example of agent-based automation for content generation, research workflows, and voice-based storytelling.

A Python project built with CrewAI that creates a podcast-style research workflow using multiple AI agents. The crew performs the following steps:

- Researches a topic using a research agent
- Converts the findings into a structured markdown report
- Writes a podcast script with two hosts
- Generates a voice-based audio file in the `outputs/` folder using Gemini TTS

This project is designed to be a practical example of a multi-agent workflow where each agent has a specific responsibility and the final output is a generated podcast script and audio.

## Project Overview

The project contains three main agents:

- `researcher`: Finds recent developments and relevant information about a topic
- `reporting_analyst`: Organizes the research into a detailed report
- `scriptwriter`: Turns the report into an engaging two-host podcast script

The execution pipeline is defined in `src/podcaster/crew.py` and the task/agent definitions live in:

- `src/podcaster/config/agents.yaml`
- `src/podcaster/config/tasks.yaml`

The custom tools used by the crew are defined in:

- `src/podcaster/tools/custom_tool.py`

## Prerequisites

Before you begin, make sure you have:

- Python 3.10 to 3.13
- `uv` installed
- Access to the following APIs:
  - OpenAI API key
  - Gemini API key
  - Serper API key

Install `uv` if you do not already have it:

```bash
pip install uv
```

## Clone the Repository

```bash
git clone https://github.com/MuhammadAwais-32013/podcaster_crew.git
cd podcaster_crew
```

## Step 1: Install Dependencies

The repo uses a Python project configuration with `pyproject.toml` and `uv.lock`.

Install the project dependencies:

```bash
uv sync
```

If you want to install the package in editable mode as well:

```bash
uv pip install -e .
```

## Step 2: Create Environment Variables

Create a `.env` file in the project root and add your keys:

```env
MODEL=gpt-4.1-mini-2025-04-14
OPENAI_API_KEY=your_openai_api_key_here
GEMINI_API_KEY=your_google_gemini_api_key_here
SERPER_API_KEY=your_serper_api_key_here
```

You may also use `GOOGLE_API_KEY` instead of `GEMINI_API_KEY` if that matches your setup.

Optional: if you use a shell environment instead of `.env`, you can export them manually:

```bash
export OPENAI_API_KEY="your_openai_api_key_here"
export GEMINI_API_KEY="your_google_gemini_api_key_here"
export SERPER_API_KEY="your_serper_api_key_here"
export MODEL="gpt-4.1-mini-2025-04-14"
```

## Step 3: Understand the Runtime Flow

The default workflow defined in `src/podcaster/main.py` uses:

```python
inputs = {
    'topic': 'AI LLMs',
    'current_month': str(datetime.now().month),
    'current_year': str(datetime.now().year)
}
```

This means the project is configured to run a podcast workflow about the topic `AI LLMs` unless you change it.

## Step 4: Run the Project

From the project root, run:

```bash
uv run podcaster
```

This entry point calls the `run()` function in `src/podcaster/main.py`.

Alternative command:

```bash
uv run crewai run
```

If the package is installed and you have the executable available, you can also run:

```bash
podcaster
```

## What Happens During Execution

When the crew runs, it does the following:

1. The `researcher` agent gathers up-to-date information on the chosen topic.
2. The `reporting_analyst` builds a markdown report from those findings.
3. The `scriptwriter` creates a natural, two-host podcast script.
4. The scriptwriter uses the Gemini voice tool to generate a `.wav` audio file.
5. Output files are saved under the `outputs/` directory.

The files are typically named like:

- `outputs/report-YYYYMMDD-HHMMSS.md`
- `outputs/script-YYYYMMDD-HHMMSS.md`
- `outputs/podcast-YYYYMMDD-HHMMSS.wav`

## Project Structure

```text
podcaster_crew/
├── README.md
├── pyproject.toml
├── uv.lock
├── src/
│   └── podcaster/
│       ├── __init__.py
│       ├── crew.py
│       ├── main.py
│       ├── config/
│       │   ├── agents.yaml
│       │   └── tasks.yaml
│       └── tools/
│           ├── __init__.py
│           └── custom_tool.py
└── outputs/
```

## Customization

You can adapt the project by editing these files:

- `src/podcaster/config/agents.yaml` — change the agent roles, goals, and backstories
- `src/podcaster/config/tasks.yaml` — change the instructions and expected output
- `src/podcaster/crew.py` — customize agents, tools, task output locations, and workflow
- `src/podcaster/main.py` — change the input topic and runtime behavior

For example, to change the topic from `AI LLMs` to something else:

```python
inputs = {
    'topic': 'AI in Healthcare',
    'current_month': str(datetime.now().month),
    'current_year': str(datetime.now().year)
}
```

## Troubleshooting

### 1. Module not found errors

Run:

```bash
uv sync
```

Then try:

```bash
uv run podcaster
```

### 2. Missing API keys

Verify that your `.env` file exists in the root folder and contains valid values:

```bash
cat .env
```

### 3. Gemini audio generation fails

Check that `GEMINI_API_KEY` or `GOOGLE_API_KEY` is correctly set and that your account has access to the Gemini model used by the script.

### 4. Serper search tool fails

Make sure `SERPER_API_KEY` is valid and has available credits.

### 5. Permission issues or output folder not created

The project creates the `outputs/` folder automatically before kickoff. If needed, make sure you have write permission in the project directory.

## Useful Commands

```bash
# Sync dependencies
uv sync

# Run the crew
uv run podcaster

# Run with crewai CLI
uv run crewai run

# View installed scripts
uv run python -m pip list
```

## License

This project does not currently specify a license in the repository metadata.

## Support

For questions about CrewAI, see:

- https://docs.crewai.com

For project-specific problems, review the config files and ensure your API keys and dependencies are valid before re-running the project.

## Summary

This project is a good example of a multi-agent system that combines research, reporting, and text-to-speech generation in a single workflow. It is particularly useful for generating topic-based podcast content from recent information and turning it into a voice-ready audio experience.
