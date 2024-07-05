---
layout: post
title:  "Como converter gratuitamente audio em texto usando inteligência artificial"
date:   2024-06-04 21:35:00 -0300
categories: [tech, dicas]
tags: [google, gmail, inteligencia-artificial]
author: "Renato Monteiro Batista"
---

# Como converter gratuitamente audio em texto usando inteligência artificial

## Instalando a extensão colaboratory no Google Drive

Esse método utiliza uma extensão que deve ser instalada no seu Google drive, logo será necessário uma conta google.

Acesse o google drive, na página inicial escolha *Novo* - *Mais* - *Conectar mais apps*.

Pesquise **Colaboratory** e instale-a no seu google drive.

Essa etapa só precisa ser realizada na primeira vez que for acessar.

## Convertendo um audio para texto usando o Colaboratory

Na página inicial do Google Drive, clique em *Novo* - *Mais* - *Google Colaboratory*.

Acesse o menu *Ambiente de execução* - *Alterar tipo de ambiente de execução*.

Selecione: *Python 3* e *T4 GPU*. Em seguida clique *Salvar*.

Insira o seguinte comando no trecho de código:

```bash
!pip install git+https://github.com/openai/whisper.git
!sudo apt update && sudo apt install ffmpeg
```

Clique no botão de play para executar e aguarde a conclusão.

Realize o upload do arquivo de áudio para o Google Colaboratory clicando no ícone de pasta ao lado esquerdo da tela. Use um nome de arquivo simplificado sem caracteres especiais ou espaços em branco.

Em seguida, insira o seguinte trecho de código:

```bash
!whisper "arquivo.mp3" --model medium
```

Lembre-se de substituir o nome do `arquivo.mp3` pelo nome do arquivo de áudio que você fez o upload.

Clique no botão de play para executar e aguarde a conclusão.