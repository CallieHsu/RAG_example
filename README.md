# RAG_example
## Environment setup
### 1. Create a Virtual Environment
```
python3 -m venv rag_example_env
```
### 2. Activate the Environment
```
source rag_example_env/bin/activate
```
### 3. Clone the Repository
```
git clone https://github.com/CallieHsu/RAG_example.git
cd RAG_example
```
### 4. Install the Packages
```
python3 -m pip install --upgrade pip
pip install -r requirements.txt
```

## Preparing LLM
- LLM format: `.gguf`
- LLM for this demo: Llama2
1. Could download from Hugging Face([TheBloke/Llama-2-7B-GGUF](https://huggingface.co/TheBloke/Llama-2-7B-GGUF)) or converted by [Llama.cpp](https://github.com/ggerganov/llama.cpp)
2. Put the `llama-2-7b-chat.Q4_K_M.gguf` into folder.


## Launch the Notebook
```
jupyter lab RAG_example.ipynb
```
