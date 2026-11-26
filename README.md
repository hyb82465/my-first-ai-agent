# My First AI Agent

A locally powered AI agent built with Hugging Face's smolagents framework, using Qwen2:7B through Ollama.

Based on the Hugging Face Agents Course starter template, this project explores local LLM integration, custom tool development, code execution, and multi-step agentic workflows.

## Features

- Local LLM inference through Ollama
- Web search using DuckDuckGo
- Time zone-based current time retrieval
- Custom inventory lookup tool
- Multi-step tool calling and calculations
- Python code generation and execution
- Third-party tool integration from Hugging Face Hub
- Interactive chat interface powered by Gradio

## Tech Stack

| Component | Technology |
|---|---|
| Language | Python 3.12 |
| Agent Framework | smolagents 1.13.0 |
| Language Model | Qwen2:7B |
| Model Runtime | Ollama |
| Model Interface | LiteLLM |
| User Interface | Gradio 5.23.1 |
| Web Search | DuckDuckGo |

## Architecture

```text
User
  |
Gradio UI
  |
CodeAgent
  |
  +-- LiteLLMModel --> Ollama --> Qwen2:7B
  |
  +-- Web Search Tool
  +-- Inventory Lookup Tool
  +-- Time Zone Tool
  +-- Image Generation Tool (Remote API)
  +-- Final Answer Tool
```

The language model runs locally, while CodeAgent manages tool selection, code execution, observations, and final responses.

External tools such as web search and image generation require network access.

## Getting Started

### 1. Install Ollama

Download and install Ollama from [ollama.com](https://ollama.com).

### 2. Download the model

```bash
ollama pull qwen2:7b
```

Make sure Ollama is running before starting the application.

### 3. Set up the Python environment

From the project directory:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 4. Run the application

```bash
python app.py
```

Open the local Gradio URL displayed in the terminal.

## Model Configuration

```python
model = LiteLLMModel(
    model_id="ollama_chat/qwen2:7b",
    api_base="http://127.0.0.1:11434",
    num_ctx=8192,
    temperature=0.5,
    max_tokens=2096,
)
```

The agent is configured with a maximum of six execution steps per run.

## Custom Tool

The project includes a custom inventory lookup tool implemented using the `@tool` decorator.

The inventory uses predefined sample data:

| Product | Quantity |
|---|---:|
| Apple | 25 |
| Banana | 10 |
| Orange | 36 |

The agent can retrieve individual stock quantities and combine multiple tool outputs through generated Python code.

## Example Tasks

| Prompt | Expected Result |
|---|---|
| Search for Python programming language. | Web search results |
| What is the stock quantity of apple? | 25 |
| What is the total stock quantity of banana and orange? | 46 |
| What is the current time in Tokyo? | Current time in Asia/Tokyo |

## Learning Outcomes

- Understanding the architecture of an AI agent
- Connecting a local language model to an agent framework
- Defining custom tools with type annotations and docstrings
- Understanding the Thought–Action–Observation cycle
- Combining multiple tool calls with Python code execution
- Debugging model-generated code and incorrect tool arguments
- Understanding how conversation history influences agent behaviour
- Integrating remote tools with a locally running language model

## Known Limitations

- Agent reliability depends on the capabilities of Qwen2:7B.
- Local inference performance depends on available hardware.
- Model-generated code may contain logical errors.
- The inventory tool uses static sample data and exact product name matching.
- Web search results may vary in relevance and availability.
- Image generation requires Hugging Face Inference Providers access and sufficient API credits. The integration was attempted, but successful image generation has not yet been verified.

## Acknowledgements

This project is adapted from the starter template provided by the [Hugging Face Agents Course](https://huggingface.co/learn/agents-course).

Resources:

- [Hugging Face Agents Course](https://huggingface.co/learn/agents-course)
- [smolagents](https://github.com/huggingface/smolagents)
- [Ollama](https://ollama.com)
- [Qwen2](https://ollama.com/library/qwen2)

This project is intended for educational and experimental purposes.
