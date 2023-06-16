---
layout: post
title:  "Do container Docker ao Dockerfile fazendo engenharia reversa de um container docker com o Dedockify"
date:   2023-06-14 13:14:15 -0300
categories: [tech, docker]
tags: [engenharia-reversa, docker]
author: "Renato Monteiro Battista"
---
O uso do containers Docker está cada vez mais popular, resolvendo o problema do "*mas roda na minha máquina*" de muitos desenvolvedores. Mas, ao mesmo tempo, coloca algumas *caixas-pretas* no ambiente computacional que **deveria** deixar qualquer pessoa sensata preocupado com segurança da informação preocupado. O que há nesses containers? Estou ingressando numa *botnet*? Ou mesmo com questões mais triviais do tipo *estou rompendo com meu desenvolvedor e preciso ter controle total dessa ferramenta sem brechas para novas modificações".

Fiz esse mesmo tipo de questionamento e minhas pesquisas me levaram até o artigo [Reverse Engineer Docker Images Into Dockerfiles](https://itnext.io/reverse-engineer-docker-images-into-dockerfiles-453d3d21d896) que explica em detalhes uma ferramenta em python para fazer a engenharia reversa de containers docker, disponível no projeto [Dedockify no Github](https://github.com/mrhavens/Dedockify).

Mas aqui não quero me ater a reescrever o artigo, mas simplesmente entregar uma solução simplificada rodando em um container docker para entregar o trabalho de fazer engenharia reversa de um container docker.

Primeiramente vamos baixar a imagem do Dedockify e criar um alias para ela no shell:

```bash
docker pull mrhavens/dedockify
alias dedockify="docker run -v /var/run/docker.sock:/var/run/docker.sock --rm mrhavens/dedockify"
```

Feito isso, vamos listar as imagens dos containers que tenho no meu repositório local:

```bash
docker image ls
```

Identificado o container em questão, vou utilizar o **IMAGE ID** no comando:

```bash
dedockify <IMAGE ID>
```

Será mostrado na tela um arquivo `Dockerfile` equivalente à aquele container. Testei em um container de um repositório privado que eu havia realizado a [transferência de containers de modo offline usando docker save e docker load](https://doc.rmbinformatica.com.br/ajuda/redes-e-infraestrutura/docker/usando-containers-docker-sem-internet-offline) e o resultado foi exatamente o mesmo que eu pude inspecionar no dockerhub como usuário autenticado.

Obviamente que em alguns casos muito específicos podem haver limitações no uso da ferramenta que não consigo identificar nem prever nesse arquivo, mas considero que é uma ferramenta que vale a pena ter sempre à mão e por isso estou documentando o uso nesse artigo.