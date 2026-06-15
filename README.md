# RAG-BASED-DOCUMENT-CHATBOT

This project implements a Retrieval-Augmented Generation (RAG) based document chatbot that runs entirely locally, meaning it does not require any external API keys (like Google Gemini, OpenAI, etc.).

## Table of Contents
- [Features](#features)
- [How it Works](#how-it-works)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [Example Document](#example-document)
- [Contributing](#contributing)
- [License](#license)

## Features
- **No API Keys**: All models (embedding and language models) run locally.
- **User File Upload**: Users can upload their own `.txt` or `.pdf` files to expand the chatbot's knowledge base.
- **Example Document Included**: Comes with a pre-loaded example document for immediate testing.
- **Interactive Chat Interface**: A simple command-line interface for natural language interaction.

## How it Works
The chatbot leverages the RAG architecture:
1.  **Document Loading & Chunking**: Documents (both pre-loaded and user-uploaded) are loaded and split into smaller, manageable chunks.
2.  **Embedding Generation**: A local `SentenceTransformer` model (`all-MiniLM-L6-v2`) converts each document chunk into a numerical vector (embedding).
3.  **Vector Store (FAISS)**: These embeddings are stored in a FAISS index, enabling fast and efficient similarity search to retrieve relevant document chunks.
4.  **Local Language Model (LLM)**: A small, open-source LLM (`distilgpt2` from Hugging Face) is used for text generation.
5.  **RAG Pipeline**: When a user asks a question:
    *   The query is embedded using the `SentenceTransformer`.
    *   The most relevant document chunks are retrieved from the FAISS vector store based on query similarity.
    *   These retrieved chunks, along with the user's original question, are fed as context into the local LLM.
    *   The LLM then generates a factual answer, grounded in the provided context.

## Setup and Installation

To run this chatbot, you'll need a Python environment. This notebook is designed to run in Google Colab.

1.  **Open in Google Colab**: You can directly open this `.ipynb` file in Google Colab.
2.  **Install Dependencies**: Run the first code cell to install the necessary libraries:
    ```bash
    !pip install transformers sentence-transformers pypdf faiss-cpu
    ```
3.  **Execute Cells**: Run all the cells in the notebook sequentially.

## Usage

1.  **Prepare Example Document**: The notebook includes a cell (`%%writefile example_document.txt`) to create a sample text file. Execute this cell to make the example document available.
2.  **Upload Your Own Documents (Optional)**: After the initial setup, you'll encounter a cell that prompts you to upload your own `.txt` or `.pdf` files. Use the Colab file uploader to add your documents. Their content will be processed and added to the chatbot's knowledge base.
3.  **Chat with the Bot**: Once all setup cells are executed, the final cell will start the interactive chatbot. Type your questions at the `You:` prompt. To exit the chat, type `exit`.

    ```
    --- Chatbot Ready! Type 'exit' to quit.---

    You: What are the benefits of exercise?
    Chatbot: Context: Regularly, exercise boosts energy levels, making daily tasks feel less daunting.
    ```

*Note: The `distilgpt2` model is lightweight and suitable for local execution, but its generation quality might be limited compared to larger models. For more sophisticated responses, consider integrating a more powerful local LLM if your computing resources allow.*

## Example Document
An `example_document.txt` describing the benefits of regular exercise is automatically created when you run the notebook.

## Contributing
Feel free to fork this repository, open issues, or submit pull requests to improve the chatbot.

## License
This project is open-source and available under the MIT License.
