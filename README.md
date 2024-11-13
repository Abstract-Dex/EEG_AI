# AI Assistant for Product Related Queries

## Overview

This document provides a detailed explanation of a Retrieval Augmented Generation (RAG) system designed for retrieving and answering queries about product information. The system utilizes a combination of OpenAI’s language models, Redis for vector embeddings, and a custom FastAPI application. The code maintains conversation memory, fetches product data from an API, generates embeddings for similarity search, and answers questions with context-aware responses.

The system performs the following tasks:

- Data Retrieval: Fetches product data from an API.
- Vector Embedding Creation: Generates vector embeddings of product data and stores them in Redis.
- Conversation System with Memory: Maintains a limited chat history, enabling memory across conversation turns.
- Query Processing and Response Generation: Answers queries related to products using a combination of information retrieval and language model generation.

## Technologies Used

1. **OpenAI Embeddings**: A library for generating vector embeddings.
2. **Redis**: A vector database for storing embeddings.
3. **Langchain**: A library for invoking language models.
4. **OpenAI GPT**: A large language model for generating responses.
5. **FastAPI**: A web framework for building APIs.

## Usage

1. Clone the repository
2. Install the required packages using the following command:

```bash
pip install -r requirements.txt
```

3. Run the following command to start the FastAPI server:

```bash
uvicorn rag:app --reload
```

4. Use Postman or any other API testing tool to send a POST request to the endpoint.

Note: For the full documentation, refer to the `ai_doc.md` file.
