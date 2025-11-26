# Agentic-RAG-Chatbot-with-CrewAI

# Agentic RAG Chatbot with CrewAI

## Description

This project is an interactive chatbot that answers questions about PDF documents. It uses a powerful technique called Retrieval-Augmented Generation (RAG) to provide accurate answers. Users can upload a PDF, and the application will use a team of AI agents, built with `crewai`, to find the most relevant information within the document and generate a comprehensive response.

The application is built using Python with the Streamlit library for the user interface and `crewai` for orchestrating the AI agents.

## How It Works

The core of this application is a multi-agent system managed by `crewai`. When you ask a question, a "crew" of AI agents collaborates to find the best possible answer from the uploaded PDF.

1.  **PDF Indexing:** When you upload a PDF, the system processes and indexes its content using the `GroundX` service. This allows for efficient searching.
2.  **User Question:** You ask a question through the web interface.
-   **Retrieval Agent:** The first agent, the **Retriever**, receives your question. Its sole job is to search the indexed PDF document for the most relevant text chunks that could answer your question. If it cannot find the information within the PDF, it will then use a web search tool as a fallback to gather information from the internet.
4.  **Response Synthesizer Agent:** The second agent, the **Response Synthesizer**, takes the relevant text provided by the Retriever. It then uses its language model capabilities to analyze this context and formulate a clear, human-readable answer.
5.  **Display Answer:** The final answer is displayed in the chat interface.

This division of labor ensures that the answers are not just guesses but are grounded in the content of the document you provide.

## Features

-   **Interactive Chat Interface:** A user-friendly web UI built with Streamlit.
-   **PDF Upload:** Easily upload your own PDF documents for analysis.
-   **AI-Powered Q&A:** Leverages `crewai` and Large Language Models for intelligent question-answering.
-   **Configurable Agents:** The behavior of the AI agents can be easily modified through YAML configuration files without changing the underlying code.

## Getting Started

Follow these steps to set up and run the project on your local machine.

### 1. Prerequisites

-   Python 3.8 or higher
-   `pip` for package management

### 2. Clone the Repository

```bash
git clone <repository-url>
cd <repository-directory>
```

### 3. Set Up a Virtual Environment

It's highly recommended to use a virtual environment to manage project dependencies.

```bash
# For Windows
python -m venv rag_env
rag_env\Scripts\activate

# For macOS/Linux
python3 -m venv rag_env
source rag_env/bin/activate
```

### 4. Install Dependencies

Install all the required Python packages using the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

### 5. Configure API Keys

The application requires API keys for the document search service (GroundX) and the web search tool (Serper). The Large Language Model (DeepSeek) is intended to be run locally via Ollama.

1.  **Ollama Setup**: Ensure you have [Ollama](https://ollama.com/) installed and the `deepseek-r1:7b` model pulled. You can pull the model using the command: `ollama pull deepseek-r1:7b`. Make sure Ollama is running before starting the application.
2.  Create a file named `.env` in the root directory of the project.
3.  Add your API keys to the `.env` file in the following format:

    ```
    GROUNDX_API_KEY="your_groundx_api_key_here"
    SERPER_API_KEY="your_serper_api_key_here"
    ```

    **Note:** You must replace the placeholder text with your actual API keys. The `DEEPSEEK_API_KEY` is not required as the model is served locally via Ollama.

## Usage

Once the setup is complete, you can run the Streamlit application with the following command:

```bash
streamlit run app_deepseek_rag.py
```

This will start a local web server, and you can access the application by navigating to the URL provided in your terminal (usually `http://localhost:8501`).


## Configuration

The `crewai` agents and their tasks are defined in the following YAML files:

-   `src/agentic_rag/config/agents.yaml`: Defines the `role`, `goal`, and `backstory` for each agent.
-   `src/agentic_rag/config/tasks.yaml`: Defines the instructions for the tasks assigned to the agents.

You can modify these files to experiment with different agent behaviors, roles, or task descriptions to fine-tune the application's performance.

## Technologies Used

-   **Python:** The core programming language.
-   **Streamlit:** For creating the interactive web user interface.
-   **CrewAI:** For orchestrating the multi-agent AI system.
-   **GroundX:** The external service used for indexing and searching PDF documents.
-   **DeepSeek:** The Large Language Model, run locally via Ollama.
-   **Ollama:** For serving the DeepSeek LLM locally.
-   **Serper:** The web search service used by `SerperDevTool` as a fallback.
