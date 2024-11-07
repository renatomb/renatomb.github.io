---
layout: post
title:  "Converta Áudio em Texto com Whisper da OpenAI, de maneira local usando a sua própria placa de vídeo"
date:   2024-11-06 19:26:00 -0300
categories: [tech, dicas]
tags: [inteligencia-artificial, convertsao, audio, texto, openai, whisper, ai, ia, artificial-inteligence, speech-to-text]
author: "Renato Monteiro Batista"
---

**Whisper** é uma ferramenta incrível da OpenAI que permite converter facilmente arquivos de áudio em texto. Com suporte para diversos idiomas e uma potência impressionante, você pode rodá-lo completamente offline no seu próprio computador, sem custos adicionais. A única despesa é ter um computador adequado e energia.

## Pré-requisitos

Para instalar o Whisper, você precisa ter o Python instalado. Recomenda-se uma placa de vídeo Nvidia com suporte a CUDA para acelerar o processo.

1 - **Verifique a versão Python**: Abra o Prompt de Comando e digite `python -V` para verificar se o Python está instalado. A versão recomendada é a 3.9.9.
2 - **Baixe o Python**: Se necessário, baixe o [instalador do Python 3.9.9 (64-bit) do site oficial](https://www.python.org/downloads/release/python-399/). Certifique-se de marcar a opção “Add to PATH” durante a instalação.
3 - **Configuração do PATH**: Adicione o caminho do Python e da pasta **Scripts** ao PATH do sistema.

### Múltiplas versões do Python

Você pode executar múltiplas versões do python na mesma máquina, desde que instalados em diretórios diferentes e configurados no path. Caso use múltiplas versões recomendo criar uma cópia do executavel `python.exe` para `python39.exe` para evitar conflitos.

### Instalação do CUDA

Verifique no site do [PyTorch](https://pytorch.org/get-started/locally/) qual a versão do CUDA necessária. No momento que estou escrevendo esse artigo a versão mínima necessária é a 11.8 e a máxima suportada é a 12.4, optei por [baixar e instalar o CUDA 11.8 do site da Nvidia](https://developer.nvidia.com/cuda-11-8-0-download-archive).

Este passo é muito importante pois caso você não tenha o CUDA instalado ou com uma versão incompatível, o PyTorch irá instalar a versão CPU do PyTorch, que é muito mais lenta.

### Instalação do PyTorch

No próprio site do PyTorch vai ter a linha de comando necessária para instalar:

```
python39 -m pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

### Verificando se o PyTorch foi instalado corretamente com o cuda

```python
import torch
print(torch.cuda.is_available())  # Deve retornar True
```

### Instale o ffmpeg

Existem várias formas de instalar o ffmpeg, desde a compilação a partir do código fonte até a instalação de pacotes pré-compilados. [Visite o site oficial ffmpeg](https://ffmpeg.org/download.html#build-windows), para todas as informações detalhadas. Nesse artigo vou optar pela instalação utilizando o Winget.

```
winget install "FFmpeg (Essentials Build)"
```

Uma das vantagens desse método é que o ffmpeg já será inserido automaticamente no PATH.

### Instale o rust

Você pode instalar o Rust através do [site oficial](https://www.rust-lang.org/tools/install) ou através do gerenciador de pacotes do Python.

```
pip3.9 install setuptools-rust
```

## Instalação do Whisper

Finalmente, atendidos todos os requisitos, podemos instalar o o Whisper com o comando:

```
pip3.9 install git+https://github.com/openai/whisper.git
```

Ao final da instalação ele informará o caminho do whisper para que você possa adicionar ao PATH, no meu caso o caminho ficou `%appdata%\Python\Python39\Scripts`. Você pode adicionar esse caminho ao seu PATH ou copiar os arquivos para a pasta `Script` que já adicionamos anteriormente.

## Usando o Whisper

Para transcrever um arquivo de áudio, abra o terminal na pasta onde o arquivo está localizado e execute:

```
whisper --model medium "seuarquivo.mp3"
```

Isso gerará arquivos nos formatos srt, vtt e txt7.

Espero que isso ajude! Se precisar de mais alguma coisa, é só avisar.

## Veja também

- [Github do projeto Whisper da OpenAI](https://github.com/openai/whisper)
- [Transcreva áudio em texto online utilizando o dupdub](https://app.dupdub.com/transcription)
- Este artigo foi inspirado no [Troublechute - Whisper Installation Guide](https://hub.tcno.co/ai/whisper/install/)