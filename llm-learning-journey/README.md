# LLM Learning Journey

A structured, hands-on repository to document my learning about **Large Language Models (LLMs)** using Python and Google Gemini.

I am building this repository step by step. Each topic will include notes, runnable code, experiments, and small projects so that I can track my progress and revise concepts for interviews.

## Learning goals

- Understand how LLM-powered applications work.
- Learn prompt engineering and model/API interaction.
- Build practical applications using Python and Gemini.
- Gradually explore embeddings, vector databases, Retrieval-Augmented Generation (RAG), agents, and evaluation.

## Repository structure

```text
llm-learning-journey/
│
├── README.md
├── requirements.txt
├── .gitignore
├── .env.example
│
├── notebooks/
│   └── 01_gemini_llm_and_recipe_generator.ipynb
│
└── src/
    └── (Python modules and reusable code will be added here)
```

### Folder guide

| Path | Purpose |
|---|---|
| `notebooks/` | Learning notebooks, experiments, explanations, and outputs |
| `src/` | Reusable Python code as the repository grows |
| `requirements.txt` | Python packages required for the examples |
| `.env.example` | Shows which environment variables are needed, without exposing secrets |
| `.gitignore` | Prevents secrets, virtual environments, and temporary files from being committed |

## Day 01 — First LLM output with Google Gemini

**Notebook:** [`01_gemini_llm_and_recipe_generator.ipynb`](notebooks/01_gemini_llm_and_recipe_generator.ipynb)

### Topics covered

#### 1. What is an LLM?

A Large Language Model is an AI model trained on large amounts of text so it can understand and generate language. In this lesson, I used an LLM through an API rather than training a model myself.

#### 2. Installing packages

```bash
pip install google-genai python-dotenv
```

- `google-genai` provides the Python SDK for calling Gemini.
- `python-dotenv` helps load environment variables from a local `.env` file.

#### 3. Environment variables and API-key safety

The API key is stored outside the notebook in a local `.env` file:

```text
GEMINI_API_KEY=your_gemini_api_key
```

Python loads it with:

```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("GEMINI_API_KEY")
```

**Security rule:** Never commit `.env`, paste API keys into notebooks, or share them in screenshots. The `.gitignore` file in this repository excludes `.env`.

#### 4. Initializing the Gemini client

```python
from google import genai

client = genai.Client(api_key=api_key)
```

The `client` object is then used to send requests to Gemini. If Python reports `NameError: name 'client' is not defined`, run the cell that creates `client` before running code that uses it.

#### 5. Sending a prompt to Gemini

```python
response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Explain LLMs in simple English."
)

print(response.text)
```

The prompt is the input instruction. `generate_content()` sends it to the selected model, and `response.text` reads the generated text. Model IDs and availability can change, so check the current Gemini API documentation if a model is unavailable.

#### 6. Python function: recipe generator

The notebook defines:

```python
def generate_recipe(ingredients: list[str], cuisine: str, diet: str) -> str:
    ...
```

Inputs:
- `ingredients`: list of available ingredients.
- `cuisine`: desired cuisine, such as Indian or Italian.
- `diet`: dietary preference, such as vegetarian, vegan, Jain, non-vegetarian, or Any.

The function builds a prompt with an f-string and sends it to Gemini.

**Python concept learned — `join()`:**

```python
ingredients = ["tomato", "onion", "chilli"]
ingredient_text = ", ".join(ingredients)
print(ingredient_text)
# tomato, onion, chilli
```

Use `join()` on a list of strings to create a readable ingredient line. Applying `join()` to a plain string would join its characters instead.

### Day 01 workflow

```text
Install packages
      ↓
Store API key in .env
      ↓
Load environment variables
      ↓
Initialize Gemini client
      ↓
Write a prompt
      ↓
Call generate_content()
      ↓
Read response.text
      ↓
Build and test a reusable recipe function
```

### Practice / next improvements

- [ ] Try different cuisines and ingredients.
- [ ] Add input validation for empty ingredients.
- [ ] Add a `max_words` parameter.
- [ ] Ask for structured output with recipe name, ingredients, and steps.
- [ ] Add a simple user interface for the recipe generator.

## Planned learning roadmap

This is the planned sequence for future learning. Items below are **planned**, not yet completed.

| Stage | Topic | Planned hands-on work |
|---|---|---|
| 1 | LLM fundamentals | Tokens, context window, temperature, model input/output |
| 2 | Prompt engineering | Zero-shot, few-shot, role/task/context, output constraints |
| 3 | Gemini API | Chat, multi-turn conversations, system instructions |
| 4 | Structured outputs | JSON responses, schemas, validation with Pydantic |
| 5 | Embeddings | Semantic similarity and vector representations |
| 6 | Vector databases | Store and retrieve relevant text chunks |
| 7 | RAG | Build a document question-answering application |
| 8 | Tools and function calling | Let a model request application functions |
| 9 | AI agents | Tool use, planning, state, and controlled workflows |
| 10 | Evaluation and safety | Test quality, grounding, errors, and prompt injection risks |
| 11 | Deployment | Build an API with FastAPI and deploy a small LLM app |

## Setup instructions

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/llm-learning-journey.git
cd llm-learning-journey
```

### 2. Create and activate a virtual environment (recommended)

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS / Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure the API key

Copy `.env.example` to `.env` and add your Gemini API key:

```text
GEMINI_API_KEY=your_real_key_here
```

Get a key from [Google AI Studio](https://aistudio.google.com/apikey).

### 5. Start Jupyter

```bash
jupyter notebook
```

Open `notebooks/01_gemini_llm_and_recipe_generator.ipynb` and run the cells from top to bottom.

## Requirements

- Python 3.10+
- A Gemini API key
- Internet connection for Gemini API requests
- Jupyter Notebook (or JupyterLab)

## Progress tracker

- [x] Day 01 — First LLM output with Gemini and a recipe generator
- [ ] Day 02 — LLM fundamentals and prompt engineering
- [ ] Day 03 — Multi-turn chat with Gemini
- [ ] Day 04 — Structured output and JSON
- [ ] Day 05 — Embeddings and semantic search
- [ ] Day 06 — Vector databases
- [ ] Day 07 — Build a basic RAG application

Update this checklist as each topic is completed.

## Learning log format for future days

For each new topic, add a notebook and update the README with:

1. **What I learned** — short explanation in my own words.
2. **Important concepts** — definitions and key points.
3. **Code examples** — small runnable examples.
4. **Experiment** — what I tried and what happened.
5. **Errors and fixes** — problems encountered and solutions.
6. **Practice tasks** — exercises to reinforce learning.
7. **References** — official documentation and useful learning resources.

## Useful resources

- [Google Gemini API documentation](https://ai.google.dev/gemini-api/docs)
- [Google Gen AI Python SDK](https://github.com/googleapis/python-genai)
- [Python documentation](https://docs.python.org/3/)
- [python-dotenv documentation](https://pypi.org/project/python-dotenv/)
- [Jupyter documentation](https://jupyter.org/documentation)

## Note

This repository is a personal learning journal and practical project collection. Code and notes will evolve as I learn more. Always check official documentation for current model names, SDK behavior, pricing, and API limits.
