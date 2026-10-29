# Langchain Gemini Agent

A LangChain-powered data analysis agent built with Google Gemini that lets you query and analyze your Titanic dataset using natural language, instead of writing manual pandas code.

## Project Structure

```
Langchain-Agent/
├── lanchain_agent_gemini.ipynb   # Jupyter notebook with the agent setup
├── titanic dataset.csv           # Titanic passenger dataset
├── requirements.txt              # Python dependencies
├── .gitignore                    # Git ignore rules
└── README.md                     # This file
```

## What This Project Does

Instead of manually writing pandas code to clean, filter, aggregate, and explore the Titanic dataset, you use a LangChain agent backed by Google Gemini. You ask questions in plain English (e.g., "What was the survival rate by passenger class?") and the agent:

- Loads the CSV into a pandas DataFrame
- Writes and executes the pandas code needed to answer your question
- Returns the result

## Manual Data Cleaning vs. LangChain Agent

| Task                        | Manual Data Cleaning (Pandas)                       | LangChain Gemini Agent                          |
| --------------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **Approach**          | You write every line of pandas code yourself        | You ask a question in natural language          |
| **Filtering**         | `df[df['Survived'] == 1]`                         | "How many passengers survived?"                 |
| **Grouping**          | `df.groupby('Pclass')['Survived'].mean()`         | "What is the survival rate by class?"           |
| **Missing values**    | `df['Age'].fillna(df['Age'].median())`            | Handled automatically by the agent              |
| **Code required**     | You must know pandas syntax & API                   | No pandas knowledge needed                      |
| **Speed (setup)**     | Fast for simple, one-off tasks                      | Slower first run (LLM + code gen)               |
| **Speed (iteration)** | Slow — rewrite code for every new question         | Fast — just ask a new question                 |
| **Errors**            | Syntax errors you must debug yourself               | Agent generates code; may need retry            |
| **Best for**          | Exploration you fully control, production pipelines | Ad-hoc analysis, non-technical users, rapid Q&A |

## Installation

1. Clone the repo:

   ```bash
   git clone https://github.com/mahak-025/Langchain-Gemini-Agent.git
   cd Langchain-Gemini-Agent
   ```
2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```
3. Set up your Google API key in a `.env` file:

   ```
   GOOGLE_API_KEY=your_api_key_here
   ```
4. Open the notebook:

   ```bash
   jupyter notebook lanchain_agent_gemini.ipynb
   ```

## Requirements

```
pandas==3.1.0
numpy==2.5.4
langchain-experimental==0.4.2
langchain-google-genai==4.4.2
langchain==0.3.0
langchain-community==0.4.2
langchain-core==1.7.1
tabulate==0.10.0
watermark==2.4.2
python-dateutil==2.9.0.post0
```

## Usage

Open `lanchain_agent_gemini.ipynb` and run the cells. The notebook sets up:

- `pandas` for data handling
- `langchain_experimental.agents.create_pandas_dataframe_agent` — the pandas agent
- `langchain_google_genai.ChatGoogleGenerativeAI` — the Google Gemini LLM

Then pass your Titanic DataFrame and the Gemini LLM to the agent and start asking questions.

## Notes

- `langchain-experimental` is sunset/no longer actively maintained. For production, consider migrating to the official LangChain agents.
- The `.env` file containing your Google API key is gitignored and never committed.
- `titanic dataset.csv` is included in the repo for immediate use.
