# RAG_WITH_GEMINI

# 📄 Chat with PDFs

This project is a **Conversational AI system** powered by **Retrieval-Augmented Generation (RAG)**. It allows users to upload PDF documents and interactively ask questions about the content. The system intelligently retrieves the most relevant information from the documents and provides detailed, context-aware answers using **Google Gemini AI**.

##  Key Features:
- **Conversational Question Answering**: Upload any PDF and get answers to your questions in natural language.
- **Powered by RAG**: Combines the power of **retrieval** (using FAISS) and **generation** (using Google’s Gemini AI) to give accurate, context-driven answers.
- **Google Generative AI Embeddings**: Efficiently processes large amounts of text and creates embeddings to enable fast and relevant searches.
- **Simple Streamlit Interface**: Intuitive and easy-to-use interface where users can upload multiple PDF files and interact with them.
- **Seamless Document Processing**: Automatically reads, processes, and splits PDF content for efficient question answering.

##  How It Works:
1. **Upload PDFs**: The user uploads one or more PDF documents through the sidebar.
2. **Text Extraction & Chunking**: The system extracts the text from the PDF files and breaks it into manageable chunks.
3. **Vector Store Creation**: These chunks are embedded using **GoogleGenerativeAIEmbeddings** and stored in a **FAISS vector store** for quick retrieval.
4. **Ask Questions**: The user can ask any question, and the system retrieves relevant information from the PDFs and generates a detailed answer using **Google’s Gemini AI**.
5. **Accurate Answers**: If the information isn't present in the document, the system will inform the user accordingly, ensuring no misleading answers.

## 🛠️ Technology Stack:
- **Streamlit**: For the user interface.
- **PyPDF2**: For PDF text extraction.
- **LangChain**: For managing text chunking and prompt chaining.
- **FAISS**: To efficiently store and search document embeddings.
- **Google Generative AI (Gemini)**: For generating natural language responses.
- **dotenv**: To manage API keys securely.

##  Getting Started:
### 1. Clone the Repository:

use this AIP: GOOGLE_API_KEY = "AIzaSyCOEzCXQ44akT2I33Ipr5RrOjgXPk8dGfc"

![Screenshot](https://github.com/Rajeshdogra/Chat-with-PDF/blob/main/screenshot%20and%20video/image.png)
```bash
git clone https://github.com/your-username/chat-with-pdf
cd chat-with-pdf


Model Architecture and Approach
1.	Model Architecture: The Retrieval-Augmented Generation (RAG) model is built to provide detailed answers to financial questions by utilizing a combination of pre-trained language models (LLMs) and a retrieval-based mechanism. The architecture is composed of the following components:
o	PDF Data Extraction: Text is extracted from uploaded PDF files using the PyPDF2 library.
o	Text Chunking: The extracted text is split into smaller, manageable chunks using RecursiveCharacterTextSplitter to prepare for efficient indexing and retrieval.
o	Vectorization: The chunks of text are transformed into embeddings using GoogleGenerativeAIEmbeddings. These embeddings allow semantic understanding and matching of the content for query responses.
o	Vector Store: The embeddings are stored in a FAISS vector store, allowing efficient similarity searches over the text data. FAISS (Facebook AI Similarity Search) is an open-source library used to perform fast similarity searches.
o	Generative Model: The model uses Google Generative AI (gemini-pro model) to generate context-based responses based on the retrieved relevant documents.
o	Question Answering: The QA chain, powered by Langchain, combines the retrieved documents with the question to provide detailed answers.
2.	Data Extraction and Preprocessing:
o	PDF Text Extraction: The PyPDF2.PdfReader is used to read the PDF documents and extract the text from each page. Any embedded or scanned content that is not selectable text may not be extracted correctly.
o	Text Chunking: The extracted text is split into smaller chunks (e.g., 10,000 characters with 1,000-character overlap) to improve the efficiency of text search and to ensure that the generative model can handle the context effectively without running out of token limits.
o	Vectorization: Each text chunk is embedded into a vector representation using Google Generative AI embeddings. The embeddings capture the semantic meaning of the text, allowing for effective similarity search during user queries.
3.	Generative Response Creation: When a user inputs a question, the model performs the following:
o	The query is passed to the vector store to retrieve the most relevant documents based on semantic similarity.
o	The relevant documents are then passed to the Google Generative AI model, along with the user query, to generate a comprehensive and contextually relevant response.
o	The model attempts to generate a detailed response, ensuring that it does not provide answers outside the context of the provided documents (if the answer is not available, it will explicitly state so).
Challenges Encountered and Solutions Implemented
1.	Challenge: Handling Non-Text PDF Files
o	Issue: Some PDF files contain images or scanned content, which cannot be extracted as text using traditional methods.
o	Solution: We implemented checks to verify whether the text extraction is successful. For cases with non-extractable text, additional steps such as Optical Character Recognition (OCR) can be implemented (e.g., using Tesseract OCR).
2.	Challenge: Large Document Size
o	Issue: PDF documents can be quite large, leading to performance issues during text chunking and vectorization.
o	Solution: The text is split into smaller chunks using the RecursiveCharacterTextSplitter to ensure that each chunk is manageable and does not exceed the token limits of the generative model. The overlap of 1,000 characters ensures that the context is preserved across chunks.
3.	Challenge: Optimizing Retrieval Speed
o	Issue: Searching through large document embeddings could become slow and inefficient, especially when there are thousands of text chunks.
o	Solution: We use FAISS (Facebook AI Similarity Search) to index and perform fast nearest-neighbor search, ensuring that the most relevant document chunks are retrieved quickly for generating responses.
4.	Challenge: Model's Understanding of Complex Financial Queries
o	Issue: The generative model might struggle with specific or complex financial terminologies, leading to incorrect or vague responses.
o	Solution: The model is fine-tuned on a financial corpus to improve its accuracy and understanding of domain-specific language. Additionally, using context from multiple related chunks helps in generating better responses.


 Guide users on how to upload documents, ask questions, and interpret the bot’s responses. 
How to Use
Step 1: Upload PDFs
1.	Click on the Upload your PDF Files button in the sidebar.
2.	Select one or more PDF files from your device.
3.	Click on Submit & Process to extract and store the text for querying.
4.	Wait for the processing to complete (indicated by a success message).
Step 2: Ask Questions
1.	In the main application window, locate the Ask a Question from the PDF Files input box.
2.	Type your question and press Enter.
Step 3: Interpret Responses
•	The bot provides answers based strictly on the uploaded documents.
•	If the answer is not found in the document, it will respond with: "Answer is not available in the context."
•	The responses aim to be as detailed as possible while staying relevant to the context.






