# Agentic Chatbot with Web Search using LangGraph

This project is an agentic chatbot built with LangGraph that can search the web to answer user queries. It utilizes Python, LangChain, and Streamlit to create a web-based conversational AI.

## Features

-   **Web Search:** The chatbot can search the web to find information to answer user queries.
-   **Conversational AI:** The chatbot can engage in conversations with users.
-   **Streamlit Interface:** The project includes a web-based user interface built with Streamlit.
-   **Powered by LangGraph:** The core agent logic is built using LangGraph, allowing for the creation of complex, stateful, and multi-agent workflows.

## Getting Started

### Prerequisites

-   Python 3.7+
-   An OpenAI API key
-   A Tavily API key
-   A Groq API key

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/akshay-kamath/Data-Science-and-Generative-AI-End-to-End-Projects.git
    cd Data-Science-and-Generative-AI-End-to-End-Projects/Agentic-Chatbot-With-Web-Search
    ```
2.  **Install the required dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Set up your environment variables:**
    Create a `.env` file in the root of the project and add your API keys:
    ```
    OPENAI_API_KEY="<your_openai_api_key>"
    TAVILY_API_KEY="<your_tavily_api_key>"
    GROQ_API_KEY="<your_groq_api_key>"
    ```

## How to Run the Application

To run the chatbot, execute the following command from the root directory of the project:

```bash
streamlit run app.py
```

This will start the Streamlit web server and open the chatbot interface in your browser. You can then interact with the chatbot by typing your questions into the input box.

## Project Structure

```
.
├── app.py
├── requirements.txt
└── src
    ├── __init__.py
    └── langgraphagenticai
        ├── __init__.py
        ├── main.py
        ├── LLMS
        │   ├── __init__.py
        │   └── groqllm.py
        ├── graph
        │   ├── __init__.py
        │   └── graph_builder.py
        ├── nodes
        │   ├── __init__.py
        │   ├── basic_chatbot_node.py
        │   └── chatbot_with_Tool_node.py
        ├── state
        │   ├── __init__.py
        │   └── state.py
        ├── tools
        │   ├── __init__.py
        │   └── search_tool.py
        └── ui
            ├── __init__.py
            ├── uiconfig.ini
            ├── uiconfig.py
            └── streamlitui
                ├── __init__.py
                ├── display_result.py
                └── loadui.py
```

### File and Folder Explanations

-   **`app.py`**: The main entry point for the Streamlit application. It initializes the UI and handles the user interaction flow.
-   **`requirements.txt`**: A list of all the Python dependencies required to run the project.
-   **`src`**: The main source code directory.
    -   **`langgraphagenticai`**: The core Python package for the agentic chatbot.
        -   **`main.py`**: This script orchestrates the entire process. It initializes the agent, the graph, and the tools, and then runs the main application loop.
        -   **`LLMS`**: This directory is responsible for managing the connection to and configuration of the Large Language Models.
            -   `groqllm.py`: Contains the specific implementation and configuration for using the Groq language model, known for its high-speed inference.
        -   **`graph`**: This directory defines the structure of the agent's decision-making process using LangGraph.
            -   `graph_builder.py`: This crucial file constructs the computational graph. It defines the nodes and the edges between them, dictating the flow of logic and data.
        -   **`nodes`**: Each file in this directory represents a node in the LangGraph. A node is a specific function or step in the agent's workflow.
            -   `basic_chatbot_node.py`: A simple node for handling basic conversational turns.
            -   `chatbot_with_Tool_node.py`: A more complex node that can decide to use external tools (like web search) to gather information before responding.
        -   **`state`**: This directory manages the state of the conversation.
            -   `state.py`: Defines the `AgentState` class, which is a data structure that keeps track of the conversation history, intermediate steps, and other important information as it flows through the graph.
        -   **`tools`**: This directory contains the tools that the agent can use to interact with the outside world.
            -   `search_tool.py`: Implements the web search functionality, likely using the Tavily API, allowing the agent to find up-to-date information.
        -   **`ui`**: This directory contains all the code related to the user interface.
            -   `uiconfig.ini` & `uiconfig.py`: Files for configuring the visual elements and settings of the UI.
            -   **`streamlitui`**: The sub-package containing the Streamlit-specific UI code.
                -   `display_result.py`: A component for rendering the chatbot's final response and any search results in the Streamlit interface.
                -   `loadui.py`: A script responsible for setting up the main layout of the Streamlit application, including titles, input boxes, and buttons.

## Dependencies

The project relies on several key Python libraries:

-   **`streamlit`**: For creating the interactive web-based user interface.
-   **`langchain`** & **`langchain-openai`**: The core framework for building LLM-powered applications.
-   **`langgraph`**: For creating robust, stateful, and agentic applications with LLMs.
-   **`langchainhub`**: To pull pre-made prompts and components from the LangChain community hub.
-   **`tavily-python`**: The Python client for the Tavily Search API.
-   **`python-dotenv`**: For managing environment variables (like API keys) securely.
-   **`groq`**: The Python client for the Groq API, enabling fast LLM inference.

All dependencies are listed in the `requirements.txt` file for easy installation.
