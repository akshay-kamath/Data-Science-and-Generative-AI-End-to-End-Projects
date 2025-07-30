# Autonomous AI Blog Writer: An End-to-End Agentic System

This project showcases a sophisticated, end-to-end autonomous AI system designed to generate high-quality, well-researched blog posts on any given topic. This is not just a simple text generator; it's a multi-agent workflow built with **LangGraph** that mimics a professional content creation team, from initial research to final publication-ready text.

The application is served via a scalable **FastAPI** backend, demonstrating a full-stack approach to deploying modern AI solutions.

## Core Features & Technical Highlights

*   **Autonomous Agentic Workflow:** The system operates as a team of specialized AI agents that collaborate to produce content. This showcases an advanced understanding of agent-based architecture.
    *   **Researcher Agent:** Dynamically searches the web using the Tavily API to gather relevant, up-to-date information and sources for the blog topic.
    *   **Writer Agent:** Takes the structured research and synthesizes it into a coherent, well-structured, and engaging blog post draft.
    *   **Editor Agent:** Critically reviews the draft for grammatical accuracy, style, tone, and factual consistency, providing feedback for revisions.
*   **Stateful Multi-Step Execution with LangGraph:** The entire workflow is modeled as a state machine using LangGraph. This allows for complex, cyclical processes where the agents can reflect, revise, and improve the content iteratively until a quality threshold is met.
*   **High-Performance Inference:** Integrated with the **Groq API** for near-instantaneous LLM inference, ensuring the application is responsive and efficient.
*   **Scalable API Backend:** Built with **FastAPI**, providing a robust, high-performance, and production-ready API for serving the blog generation service.
*   **End-to-End Solution:** This is a complete application, from the API endpoint that receives a topic to the final, polished blog post returned to the user.

## How It Works: The Agentic Process

The application's intelligence lies in its structured, graph-based workflow managed by LangGraph.

1.  **Topic Input:** The process begins when a user submits a topic via the FastAPI endpoint.
2.  **Planning & Research:** The initial agent receives the topic, plans the blog structure (e.g., introduction, key sections, conclusion), and uses the **Search Tool** to conduct web research.
3.  **Drafting:** The research findings are passed to the **Writer Agent**, which generates the first draft of the blog post.
4.  **Critique & Revision Cycle:** The draft is then passed to the **Editor Agent**. The editor evaluates the content and decides if it's ready for publication or needs revision. If revision is needed, it sends feedback back to the Writer Agent. This loop continues until the content is approved.
5.  **Final Output:** Once the Editor Agent approves the blog, the final, polished text is returned as the API response.

This entire process is orchestrated by the `graph_builder.py` which defines the nodes (agents) and edges (transitions) of the workflow.

## Getting Started

### Prerequisites

*   Python 3.8+
*   An OpenAI API Key
*   A Tavily Search API Key
*   A Groq API Key

### Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/akshay-kamath/Data-Science-and-Generative-AI-End-to-End-Projects.git
    cd Data-Science-and-Generative-AI-End-to-End-Projects/End-to-End-Blog-generation-Agentic-AI-app
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Configure Environment Variables:**
    Create a `.env` file in the project root and populate it with your API keys:
    ```
    OPENAI_API_KEY="your_openai_api_key_here"
    TAVILY_API_KEY="your_tavily_api_key_here"
    GROQ_API_KEY="your_groq_api_key_here"
    ```

### Running the Application

1.  **Start the FastAPI server:**
    ```bash
    uvicorn app:app --reload
    ```
2.  **Access the API:**
    The application will be running at `http://127.0.0.1:8000`.
    *   For interactive API documentation (via Swagger UI), navigate to `http://127.0.0.1:8000/docs`.
    *   You can send a `POST` request to the `/invoke` endpoint to start a blog generation task.

3.  **Making a Request:**
    You can use the `request.json` file as a template for your request body or use `curl`:
    ```bash
    curl -X 'POST' \
      'http://127.0.0.1:8000/invoke' \
      -H 'accept: application/json' \
      -H 'Content-Type: application/json' \
      -d '{
        "input": {
          "topic": "The Future of AI in Finance"
        }
      }'
    ```

## In-Depth Project Structure

```
.
├── app.py              # FastAPI application entry point, defines API endpoints.
├── requirements.txt    # Project dependencies.
├── pyproject.toml      # Build system configuration.
├── langgraph.json      # (Optional) A snapshot or definition of the LangGraph graph.
├── request.json        # A sample request body for testing the API.
└── src/                # Main source code module.
    ├── __init__.py
    ├── graphs/
    │   └── graph_builder.py # Core Logic: Defines the LangGraph workflow, nodes, and edges.
    ├── llms/
    │   └── groqllm.py       # Configuration and instantiation of the Groq LLM.
    ├── nodes/
    │   └── blog_node.py     # Implements the functions for each agent (research, write, edit).
    └── states/
        └── blogstate.py     # Defines the `AgentState` data structure passed between nodes.
```

## Technologies Used

*   **Backend:** FastAPI, Uvicorn
*   **AI / LLM Framework:** LangChain, LangGraph
*   **LLM Providers:** OpenAI, Groq
*   **Search API:** Tavily
*   **Dependency Management:** Pip, Poetry (`pyproject.toml`)

