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
- CUDA toolkit required  📚 [How to Install CUDA on Ubuntu 22.04 | Step-by-Step](https://www.cherryservers.com/blog/install-cuda-ubuntu)
#### **CUDA installation**
Reference: [How to Install CUDA on Ubuntu 22.04 | Step-by-Step](https://www.cherryservers.com/blog/install-cuda-ubuntu)
##### 1. Upgrade your Ubuntu
```
sudo apt update
sudo apt upgrade 
```
##### 2. List & install the recommended NVIDIA drivers
```
sudo apt install ubuntu-drivers-common
sudo ubuntu-drivers devices
```
Then install the recommended driver list above:
```
sudo apt install nvidia-driver-XXX
```
##### 3. Reboot your system & Check the driver installation
```
sudo reboot now
```
```
nvidia-smi
```
##### 4. Install GCC
```
sudo apt install gcc
```
check installation:
```
gcc -v
```
##### 5. Install CUDA toolkit Ubuntu
- Go to Nvidia CUDA Toolkit download website:

![image](https://github.com/CallieHsu/RAG_example/assets/62089495/4bf0fd71-5f6b-412d-8a32-26a9f969d07a)

- follow the steps it shows:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-4
```
If you encounter dependency errors during the installation, try running `sudo apt --fix-broken install` to fix them. Apt will suggest running it if needed.
- Reboot your system to load the right modules required by CUDA.
```
sudo reboot now
```
#### 6. Environment setup
- Add the following lines to your `~/.bashrc`, then `source ~/.bashrc`
```bash
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-12.4/lib64\
                         ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
#### 7. Test the CUDA toolkit, done !
```
nvcc -V
```
### llama-cpp-python for Nvidia GPU
```
!CMAKE_ARGS="-DLLAMA_CUBLAS=on" FORCE_CMAKE=1 pip install --upgrade --force-reinstall llama-cpp-python --no-cache-dir
```
📚 more details: [llama-cpp-python: Installation with OpenBLAS / cuBLAS / CLBlast](https://python.langchain.com/docs/integrations/llms/llamacpp/#installation-with-openblas-cublas-clblast)

### Arguments for GPU device
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
