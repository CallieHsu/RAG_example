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

### 5. (For GPU device) llama.cpp for LangChain
#### Nvidia GPU
- CUDA toolkit required  📚 [How to Install CUDA on Ubuntu 22.04 | Step-by-Step](https://www.cherryservers.com/blog/install-cuda-ubuntu)
```
!CMAKE_ARGS="-DLLAMA_CUBLAS=on" FORCE_CMAKE=1 pip install --upgrade --force-reinstall llama-cpp-python --no-cache-dir
```
📚 more details: [llama-cpp-python: Installation with OpenBLAS / cuBLAS / CLBlast](https://python.langchain.com/docs/integrations/llms/llamacpp/#installation-with-openblas-cublas-clblast)



## Preparing LLM
- LLM format: `.gguf`
- LLM for this demo: Llama2
1. Could download from Hugging Face([TheBloke/Llama-2-7B-Chat-GGUF](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGUF)) or converted by [Llama.cpp](https://github.com/ggerganov/llama.cpp)
2. Put the `llama-2-7b-chat.Q4_K_M.gguf` into folder.


## Launch the Notebook
```
jupyter lab RAG_example.ipynb
```
