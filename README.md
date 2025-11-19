# Langchain
1. ** Install Required Libraries**  
   The script installs all necessary Python packages:
   - `langchain` and `langchain-community`: For building modular LLM-powered applications.
   - `faiss-cpu`: For fast vector similarity search.
   - `pypdf`, `python-docx`: For loading PDF and Word documents.
   - `sentence-transformers`: For generating dense text embeddings.
   - `transformers`: For using Hugging Face models.

2. ** Upload a Document in Google Colab**  
   - Uses `files.upload()` to let the user upload a `.pdf`, `.docx`, or `.txt` file.
   - Extracts the filename for further processing.

3. ** Load the Document**  
   - Based on the file extension, selects the appropriate loader:
     - `PyPDFLoader` for PDFs
     - `Docx2txtLoader` for Word documents
     - `TextLoader` for plain text files
   - Loads the document into memory as a list of `Document` objects.

4. ** Split the Document into Chunks**  
   - Uses `RecursiveCharacterTextSplitter` to divide the document into overlapping chunks (500 characters with 100-character overlap) for better context retention during embedding and retrieval.

5. ** Generate Embeddings and Build Vector Store**  
   - Uses the `all-MiniLM-L6-v2` model from `sentence-transformers` to convert text chunks into vector embeddings.
   - Stores these embeddings in a FAISS vector database for efficient similarity search.

6. ** Load a Lightweight Language Model**  
   - Loads the `google/flan-t5-base` model using Hugging Face’s `pipeline` for text-to-text generation.
   - Wraps it in a `HuggingFacePipeline` to integrate with LangChain.

7. ** Create a Retrieval-Based QA Chain**  
   - Constructs a `RetrievalQA` chain that:
     - Retrieves the top 3 most relevant chunks from the vector store.
     - Feeds them into the LLM to generate an answer using the "stuff" chain type.

8. ** Run a Test Query**  
   - Executes a sample query: “Give me a short summary of the document” and prints the result.

9. ** Interactive Q&A Loop**  
   - Enters a loop where the user can ask questions about the uploaded document.
   - The loop continues until the user types `"exit"`.

