# Zoo Guide Agent

Welcome to the Zoo Guide Agent! This project demonstrates a multi-agent system built with the Google Agent Development Kit (ADK). The agent acts as a friendly and knowledgeable tour guide for a zoo, capable of answering user questions by combining internal zoo data with external knowledge from Wikipedia.

## Features

*   **Multi-Agent Architecture**: Utilizes a sophisticated workflow with multiple specialized agents:
    *   `greeter`: The main entry point that welcomes the user.
    *   `comprehensive_researcher`: Gathers information from various sources.
    *   `response_formatter`: Synthesizes data into a friendly, conversational response.
*   **Tool Integration**: Seamlessly integrates with external tools like Wikipedia to provide rich, factual information.
*   **Sequential Workflow**: Uses a `SequentialAgent` to process user requests in a logical, step-by-step manner (research first, then format the response).
*   **Google Cloud Native**: Designed to run on Google Cloud, using services like Cloud Logging and authenticating with service accounts.

## Prerequisites

Before you begin, ensure you have the following installed and configured:

*   Python 3.9+
*   Google Cloud SDK (`gcloud`)
*   A Google Cloud Project

## Setup and Installation

1.  **Clone the Repository**

    ```bash
    git clone <your-repository-url>
    cd zoo_guide_agent
    ```

2.  **Create a Python Virtual Environment**

    It's highly recommended to use a virtual environment to manage project dependencies.

    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Install Dependencies**

    Create a `requirements.txt` file with the necessary packages:

    ```text
    google-adk
    langchain-community
    wikipedia
    python-dotenv
    google-cloud-logging
    google-auth
    ```

    Then, install them using pip:

    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure Environment Variables**

    The agent is configured using a `.env` file. Your project already contains this file.

    ```properties
    PROJECT_ID=Your Projectid
    PROJECT_NUMBER=your Project number
    SA_NAME=lab2-cr-service
    SERVICE_ACCOUNT=lab2-cr-service@Your Projectid.iam.gserviceaccount.com
    MODEL="gemini-2.5-flash"
    ```

    Ensure these values are correct for your Google Cloud environment.

5.  **Google Cloud Authentication**

    Configure the `gcloud` CLI to use your project. This is a one-time setup for your environment.

    ```bash
    gcloud config set project gen-lang-client-0756045557
    ```

## How It Works

The core logic is defined in `agent.py`.

1.  The `root_agent` ("greeter") starts the conversation.
2.  When the user asks a question, their prompt is saved to the agent's state.
3.  Control is transferred to the `tour_guide_workflow`, which is a `SequentialAgent`.
4.  **Step 1**: The `comprehensive_researcher` agent analyzes the user's prompt and uses its tools (currently Wikipedia) to gather relevant facts.
5.  **Step 2**: The `response_formatter` agent takes the data collected by the researcher and crafts a user-friendly, engaging response, acting as the voice of the tour guide.

