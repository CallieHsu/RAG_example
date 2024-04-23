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
#### llama-cpp-python for Nvidia GPU
- CUDA toolkit required  📚 [How to Install CUDA on Ubuntu 22.04 | Step-by-Step](https://www.cherryservers.com/blog/install-cuda-ubuntu)
```
!CMAKE_ARGS="-DLLAMA_CUBLAS=on" FORCE_CMAKE=1 pip install --upgrade --force-reinstall llama-cpp-python --no-cache-dir
```
📚 more details: [llama-cpp-python: Installation with OpenBLAS / cuBLAS / CLBlast](https://python.langchain.com/docs/integrations/llms/llamacpp/#installation-with-openblas-cublas-clblast)

#### Arguments for GPU device
If the installation with BLAS backend was correct, you will see a `BLAS = 1` indicator in model properties.

Two of the most important parameters for use with GPU are:

- `n_gpu_layers` - determines how many layers of the model are offloaded to your GPU.
- `n_batch` - how many tokens are processed in parallel.
Setting these parameters correctly will dramatically improve the evaluation speed (see wrapper code for more details).

```python
n_gpu_layers = -1  # The number of layers to put on the GPU. The rest will be on the CPU. If you don't know how many layers there are, you can use -1 to move all to GPU.
n_batch = 512  # Should be between 1 and n_ctx, consider the amount of VRAM in your GPU.

# Make sure the model path is correct for your system!
llm = LlamaCpp(
    model_path="llama-2-7b-chat.Q4_K_M.gguf",
    n_gpu_layers=n_gpu_layers,
    n_batch=n_batch,
    callback_manager=callback_manager,
    verbose=True,  # Verbose is required to pass to the callback manager
)
```
📚 reference: [llama-cpp-python: GPU](https://python.langchain.com/docs/integrations/llms/llamacpp/#gpu)

## Preparing LLM
- LLM format: `.gguf`
- LLM for this demo: Llama2
1. Could download from Hugging Face([TheBloke/Llama-2-7B-Chat-GGUF](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGUF)) or converted by [Llama.cpp](https://github.com/ggerganov/llama.cpp)
2. Put the `llama-2-7b-chat.Q4_K_M.gguf` into folder.


## Launch the Notebook
```
jupyter lab RAG_example.ipynb
```
