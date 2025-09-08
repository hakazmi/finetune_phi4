# US Constitution Q&A Bot – Fine-tuned PHI-4 LLM


Link OF US_Constitution_dataset = https://drive.google.com/file/d/1hiBPM4158QPpV88QH3Qayj4WU7TlzpDf/view?usp=drive_link

This Jupyter Notebook implements a Q&A bot for answering questions about the US Constitution using a fine-tuned language model. The setup includes a **FastAPI backend** for model inference, a **Streamlit frontend** for user interaction, and **ngrok** for public access to both services.

---

## Overview

- **Backend:** FastAPI serves the fine-tuned model (`abdulsamad99/CONSTITUTION_USA-fine-tuning`) from Hugging Face, quantized to 4-bit for efficiency.  
- **Frontend:** Streamlit provides a chat interface for users to ask questions.  
- **Tunneling:** Ngrok exposes both FastAPI and Streamlit to public URLs.  
- **Model:** Uses Unsloth and Hugging Face Transformers for efficient inference.  
- **Purpose:** Answer questions about the US Constitution with concise, relevant responses.

---

## Prerequisites

### Hardware

- Minimum **8GB RAM**; GPU recommended for faster inference (Colab provides free GPU).  
- 4-bit quantization reduces memory needs, but a GPU with **4GB+ VRAM** is ideal.

### Software

- Python **3.8+** (tested on 3.10+).  
- Jupyter Notebook/Lab or Google Colab.  
- Hugging Face account (no token needed for public models).  
- Ngrok account: Sign up at [ngrok.com](https://ngrok.com) for two auth tokens (one for FastAPI, one for Streamlit).

### Ngrok Tokens

Obtain two tokens from your ngrok dashboard:  
- `FASTAPI_NGROK_TOKEN`: For FastAPI server.  
- `STREAMLIT_NGROK_TOKEN`: For Streamlit app.

---

## Installation

### Download Notebook

Save the `.ipynb` file (e.g., `us_constitution_qa_bot.ipynb`).

### Set Up Environment

**Locally:**  
```bash
pip install jupyter
jupyter notebook us_constitution_qa_bot.ipynb



On Colab: Upload the notebook and select a GPU runtime (Runtime > Change runtime type > GPU).


Install Dependencies:

The first notebook cell installs required packages:
unsloth, transformers, fastapi, uvicorn, streamlit, pyngrok, torch, etc.


Run the cell to install everything (may take a few minutes).



Configuration

Set Ngrok Tokens:

In the notebook, replace placeholders:FASTAPI_NGROK_TOKEN = "your_fastapi_ngrok_token_here"
STREAMLIT_NGROK_TOKEN = "your_streamlit_ngrok_token_here"


Use your actual tokens from ngrok.


Update FastAPI URL in Streamlit:

After running the FastAPI cell, it outputs a public ngrok URL (e.g., https://xxxx.ngrok-free.app).
In the %%writefile app.py cell, update:FASTAPI_URL = "your_fastapi_ngrok_url_here"


Re-run the %%writefile app.py cell to save the change.



Running the Notebook

Execute Cells:

Run cells sequentially (Shift + Enter).
Steps:
Install dependencies.
Load model and tokenizer from Hugging Face.
Start FastAPI server (on port 8000) with ngrok tunnel.
Write app.py for Streamlit.
Start Streamlit (on port 8501) with ngrok tunnel.




Outputs:

FastAPI:✅ FastAPI running locally at http://localhost:8000
🌐 FastAPI ngrok URL: https://xxxx.ngrok-free.app


Copy the ngrok URL and update FASTAPI_URL in app.py.


Streamlit:🌐 Streamlit ngrok URL: https://yyyy.ngrok-free.app


Open this URL in a browser for the chat interface.




Using the Bot:

Access the Streamlit URL.
Enter questions (e.g., "What is the First Amendment?").
Responses stream word-by-word.
Chat history is preserved in the session.


Stopping the Notebook:

Interrupt the kernel (Jupyter: Kernel > Interrupt; Colab: Stop execution).
Ngrok tunnels close automatically.
If tunnels persist, terminate them via the ngrok dashboard.



Troubleshooting

Installation Issues:

Package conflicts: Use a virtual environment:python -m venv env
source env/bin/activate
pip install -r requirements.txt  # List packages from notebook


Colab: Ensure GPU runtime is enabled.


Model Loading:

"Out of Memory": Reduce max_new_tokens or use a higher-VRAM GPU.
CPU fallback is slower but works if no GPU is available.


Ngrok Issues:

"Invalid auth token": Verify tokens in ngrok dashboard.
"Tunnel limit reached": Free ngrok accounts have limits; wait or upgrade.
Use separate tokens for FastAPI and Streamlit.


Server Issues:

FastAPI not responding: Test locally with:curl -X POST http://localhost:8000/generate -H "Content-Type: application/json" -d '{"question": "Test question"}'


Streamlit errors: Check console logs or ensure FASTAPI_URL is correct.


Response Quality:

Model is fine-tuned for US Constitution; off-topic questions may yield poor results.
Adjust max_new_tokens, temperature, or top_p in ask_model for better responses.



