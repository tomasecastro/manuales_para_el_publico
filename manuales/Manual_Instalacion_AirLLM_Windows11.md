# Manual de instalación y ejecución de AirLLM

## 1. Instalación inicial (solo la primera vez)

```powershell
pip install airllm transformers accelerate torch
pip install bitsandbytes
```

**Importante**: si `torch.cuda.is_available()` devuelve `False`, debes desinstalar la versión CPU y reinstalar la versión CUDA:

```powershell
pip uninstall -y torch torchvision torchaudio
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu126
```

Verifica antes de continuar:

```powershell
python -c "import torch; print(torch.__version__); print('CUDA:', torch.cuda.is_available())"
```

Debe mostrar algo como `2.14.1+cu126` y `CUDA: True`.

> **Nota sobre CUDA**: el CUDA Toolkit instalado desde `https://developer.nvidia.com/cuda` no es necesario para que AirLLM funcione. PyTorch (`torch` con `--index-url .../cu126`) incluye su propio runtime de CUDA. El Toolkit solo se necesita si vas a compilar código CUDA personalizado con `nvcc`.

## 2. Ejecutar AirLLM cada vez

Solo necesitas situarte en PowerShell y lanzar tu script:

```powershell
cd C:\Proyectos\airllm
python qwen.py
```

## 3. Advertencias y tiempos

- La **primera ejecución** es lenta porque descarga el modelo y genera los archivos `splitted_model.4bit` capa por capa (se guardan como `model.layers.N.safetensors`). Las siguientes ejecuciones reutilizan ese caché y arrancan mucho más rápido.
- Si la descarga se interrumpe, vuelve a ejecutar el mismo comando; AirLLM retoma donde lo dejó y re-splitea solo lo que falte.
- Para evitar el warning de peticiones no autenticadas a Hugging Face puedes definir un token:

```powershell
setx HF_TOKEN "tu_token_de_huggingface"
```

Y luego abrir una nueva PowerShell.

## 4. Comprobar estado de la GPU

```powershell
nvidia-smi
```

## 5. Resumen de una línea para el día a día

```powershell
cd C:\Proyectos\airllm; python qwen.py
```

Eso es todo lo que necesitas de aquí en adelante.
