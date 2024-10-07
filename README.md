# Sherlock.ai
Hi, this is a multi-PDF chat project using Google Gemini API. It can read multiple ePDFs and converse about their content.
Here is the demo video on YouTube - https://youtu.be/F2k814v3xgY

The code - is straightforward from an online tutorial video (Krish Naik).

**Some screenshots**

![image](https://github.com/user-attachments/assets/2b57bac6-3a4b-472d-970b-ec62eaef8b65)

![image](https://github.com/user-attachments/assets/9b60aeee-38e3-47d9-bb11-fbb134077fda)

![image](https://github.com/user-attachments/assets/2b1f31e6-fd4d-4366-835e-fd74abd8cac8)

**------Code Breakdown------**

**Imports and Configuration**

from dotenv import load_dotenv: Loads environment variables from a .env file that has sensitive information like API keys.
import google.generativeai as genai: Imports the Google Generative AI library, allowing you to use its functionalities.
import streamlit as st: Imports the Streamlit library to create a web app interface.

**PDF Handling and Text Extraction**

from PyPDF2 import PdfReader: Imports the PdfReader class from the PyPDF2 library, enabling the reading of PDF files.
def get_pdf(pdf_docs):: A function that takes a list of PDF file objects and extracts text from each page, returning the combined text as a string.

**Text Chunking**

def get_text_chunks(text):: This function splits the extracted text into smaller chunks using the RecursiveCharacterTextSplitter class, which is useful for processing long texts.
return chunks: Returns the list of text chunks for further processing.

**Creating a Vector Store-**

def get_vector_store(text_chunks):: Converts text chunks into a vector store using embeddings (numeric representations) from the Google Generative AI model.
vector_store.save_local("faiss_index"): Saves the created vector store locally for future use.

**Conversational Chain Setup**

def get_coversational_chain():: Sets up a question-answering chain using a prompt template and a chat model from Google Generative AI.
return chain: Returns the constructed chain that will be used for answering user queries.

**User Input Handling**

def user_input(user_question):: This function is called when the user inputs a question.
new_db=FAISS.load_local("faiss_index", embeddings): Loads the previously created vector store for similarity searching.
docs= new_db.similarity_search(user_question): Searches for relevant documents based on the user’s question.
response= chain(...): Calls the QA chain to generate a response based on the relevant documents found.
st.write(...): Displays the response in the Streamlit app.

**Main Function to Set Up the Streamlit App**

def main():: The main function that sets up the Streamlit web app.
if user_question:: Checks if the user has entered a question, and if so, calls user_input(user_question) to process it.
pdf_docs=st.file_uploader("Upload your pdf here"): Allows users to upload PDF files.
if st.button("Submit"):: Processes the uploaded PDFs to extract text, chunk it, and create the vector store when the user clicks the submit button.

**Execution**

if __name__ =="__main__":: Ensures that the main function runs only when the script is executed directly, not when imported as a module.
