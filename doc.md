# Chatbot with Retrieval-Augmented Generation (RAG) System

## Key Components

1. **Redis Integration**

   - The system uses Redis as a vector store to store and retrieve product information.
   - It initializes a Redis client and a custom `LimitedRedisChatMessageHistory` class to maintain a limited history of recent conversation messages.

2. **OpenAI Integration**

   - The system utilizes OpenAI's language models for embedding generation and question answering.
   - It initializes an `OpenAIEmbeddings` model for creating vector embeddings and a `ChatOpenAI` model for generating responses.

3. **Data Retrieval and Preprocessing**

   - The system fetches product data from an API, cleans and prepares the data, and creates a text corpus for the products.
   - It then generates product summaries using the ChatGPT model.

4. **Vector Store Initialization**

   - The system initializes the Redis vector store, either by retrieving an existing index or creating a new one.
   - It stores the product summaries and their metadata (such as product ID) in the vector store.

5. **Chat Interface**

   - The system defines a `ChatPromptTemplate` and a `RunnableWithMessageHistory` chain that utilizes the product data, chat history, and the language model to generate responses to user queries.

6. **API Endpoints**
   - The system exposes two API endpoints, `/api/chat` (GET and POST), that handle user chat requests.
   - The endpoints retrieve relevant product information from the vector store, pass it to the language model, and return the generated response.

## Detailed Workflow

1. **Startup Event**

   - When the application starts, the `startup_event` function is executed.
   - It initializes the Redis client and the Redis vector store (either by retrieving an existing index or creating a new one).

2. **Root and Health Endpoints**

   - The application provides two endpoints:
     - `/`: The root endpoint, which returns a simple health check response.
     - `/health`: The health check endpoint, which tests the Redis connection and returns the service status.

3. **Initialization of OpenAI Components**

   - The system initializes the OpenAI embedding model and the chat model, using the provided API key.

4. **Definition of Prompts and Templates**

   - The system defines a `question_template` for reducing the user's question to a simpler form, and a `prompt` template for the chat interface.
   - The `prompt` template includes the system prompt, the chat history, and the user's question.

5. **Chain with Message History**

   - The system creates a `RunnableWithMessageHistory` chain that combines the `prompt` template and the language model.
   - This chain also uses the `LimitedRedisChatMessageHistory` class to maintain a limited history of recent conversation messages.

6. **Data Retrieval and Preprocessing**

   - The `get_data()` function fetches the product data from an API.
   - The `prepare_data()` and `create_corpus()` functions clean and prepare the data, creating a text corpus for the products.
   - The `create_prod_summary()` function generates a summary for each product using the ChatGPT model.

7. **Vector Store Initialization**

   - The `init_redis_store()` function initializes the Redis vector store, either by retrieving an existing index or creating a new one.
   - It stores the product summaries and their metadata (such as product ID) in the vector store.

8. **Chat Endpoint**

   - The `/api/chat` endpoint (both GET and POST) handles user chat requests.
   - It retrieves the relevant product information from the vector store using the `retrieve_docs()` function, which modifies the user's question using the `question_template`.
   - It passes the user's question and the retrieved product information to the `chain_with_history` object, which generates a response using the language model and the chat history.
   - It returns the generated response as an `AnswerResponse` object.

9. **Error Handling**

   - The system includes proper error handling, raising `HTTPException` instances with appropriate status codes and error messages when issues occur.

10. **Startup and Main**
    - The application uses the `uvicorn` library to run the FastAPI application, listening on the configured port (or the default port of 8000 if not specified).
