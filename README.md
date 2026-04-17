# LangChain Academy: Introduction to LangGraph (Ollama Edition)

## Introduction

This is a fork of the [LangChain Academy](https://github.com/langchain-ai/langchain-academy) "Introduction to LangGraph" course, modified to run with **local models via [Ollama](https://ollama.com/)** instead of the OpenAI API.

### Key differences from the original course

- **`ChatOllama`** replaces `ChatOpenAI` throughout all notebooks and studio files.
- Models used: **qwen2.5:3b** (most modules) and **qwen2.5:7b** (structured output in module 5).
- No `OPENAI_API_KEY` is required for the core exercises.
- Some prompts include explicit tool-calling instructions as a workaround for local models not respecting `tool_choice` as reliably as OpenAI's API.
- Generation times can be significantly slower on consumer hardware (e.g., 10–20 minutes for complex multi-agent workflows in module 4).

This is a growing set of modules focused on foundational concepts within the LangChain ecosystem. 
Module 0 is basic setup and Modules 1 - 5 focus on building in LangGraph, progressively adding more advanced themes. Module 6 addresses deploying your agents. 
In each module folder, you'll see a set of notebooks. A link to the LangChain Academy lesson is at the top of each notebook to guide you through the topic. Each module also has a `studio` subdirectory, with a set of relevant graphs that we will explore using the LangGraph API and Studio.

## Setup

### Python version

Make sure you're using Python version 3.11, 3.12, or 3.13.
```
python3 --version
```

### Clone repo
```
git clone https://github.com/langchain-ai/langchain-academy.git
$ cd langchain-academy
```

### Create an environment and install dependencies
#### Mac/Linux/WSL
```
$ python3 -m venv lc-academy-env
$ source lc-academy-env/bin/activate
$ pip install -r requirements.txt
```
#### Windows Powershell
```
PS> python3 -m venv lc-academy-env
PS> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
PS> .\lc-academy-env\Scripts\Activate.ps1
PS> pip install -r requirements.txt
```

### Install Ollama and pull models

1. **Install Ollama** by following the instructions at [https://ollama.com/download](https://ollama.com/download).
2. **Verify** the installation:
   ```
   ollama --version
   ```
3. **Pull the required models**:
   ```
   ollama pull qwen2.5:3b
   ollama pull qwen2.5:7b
   ```
   `qwen2.5:3b` is used in most modules. `qwen2.5:7b` is used for structured output tasks in module 5.
4. Make sure the Ollama server is running before starting any notebooks. It starts automatically after installation, or you can run:
   ```
   ollama serve
   ```

### Running notebooks
If you don't have Jupyter set up, follow the installation instructions [here](https://jupyter.org/install).
```
$ jupyter notebook
```

### Setting up env variables
Briefly going over how to set up environment variables. 
#### Mac/Linux/WSL
```
$ export API_ENV_VAR="your-api-key-here"
```
#### Windows Powershell
```
PS> $env:API_ENV_VAR = "your-api-key-here"
```

### Sign up and Set LangSmith API
* Sign up for LangSmith [here](https://docs.langchain.com/langsmith/create-account-api-key#create-an-account-and-api-key), find out more about LangSmith and how to use it within your workflow [here](https://www.langchain.com/langsmith). 
*  Set `LANGSMITH_API_KEY`, `LANGSMITH_TRACING_V2="true"` `LANGSMITH_PROJECT="langchain-academy"`in your environment 
*  If you are on the EU instance also set `LANGSMITH_ENDPOINT`="https://eu.api.smith.langchain.com" as well.

### Set up Tavily API for web search

* Tavily Search API is a search engine optimized for LLMs and RAG, aimed at efficient, 
quick, and persistent search results. 
* You can sign up for an API key [here](https://tavily.com/). 
It's easy to sign up and offers a very generous free tier. Some lessons (in Module 4) will use Tavily. 

* Set `TAVILY_API_KEY` in your environment.

### Set up Studio

* Studio is a custom IDE for viewing and testing agents.
* Studio can be run locally and opened in your browser on Mac, Windows, and Linux.
* See documentation [here](https://docs.langchain.com/langsmith/studio#local-development-server) on the local Studio development server. 
* Graphs for LangGraph Studio are in the `module-x/studio/` folders for module 1-5.
* To start the local development server, make sure your virtual environment is active and run the following command in your terminal in the `/studio` directory in each module:

```
langgraph dev
```

You should see the following output:
```
- 🚀 API: http://127.0.0.1:2024
- 🎨 Studio UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
- 📚 API Docs: http://127.0.0.1:2024/docs
```

Open your browser and navigate to the Studio UI: `https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024`.

* To use Studio, you will need to create a .env file with the relevant API keys
* Run this from the command line to create these files for module 4, as an example:
```
echo "TAVILY_API_KEY=\"$TAVILY_API_KEY\"" >> module-4/studio/.env
```