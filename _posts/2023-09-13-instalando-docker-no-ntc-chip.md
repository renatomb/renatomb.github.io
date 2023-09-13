---
layout: post
title:  "Instalando o docker no NTC CHIP"
date:   2023-09-13 13:50:00 -0300
categories: [docker]
tags: [ntc, chip, docker]
author: "Renato Monteiro Batista"
---
Hoje eu tive que me aventurar na tarefa de instalar o docker no NTC CHIP, a maior dificuldade se deu devido ao fato do mesmo rodar o Debian 8 que já encerrou o ciclo de vida. Então vamos diretamente ao que foi necessário.

A princípio comecei pelo básico tentando atualizar o sistema e instalar o docker através do comando `apt-get install docker-ce`. Porém não funcionou, a atualização do sistema retornava vários erros `404  Not Found` e, por fim `E: Some index files failed to download. They have been ignored, or old ones used instead.`. Já a instalação do docker retornou `E: Unable to locate package docker-ce`.

Feito isso tentei seguir o roteiro de [Install Docker Engine on Debian](https://docs.docker.com/engine/install/debian/#install-using-the-repository) mas esbarrei em `E: The method driver /usr/lib/apt/methods/https could not be found.`. Tampouco consegui instalar o tal do apt-transport-https.

Depois de muitas indas e vindas tentando adicionar o repositório, fazer link simbólico do method driver de http para https e várias outras tentativas frustradas, encontrei o artigo [JF Possibilities' mirror of CHIP ".deb" repositories.](http://chip.jfpossibilities.com/chip/debian/) que me esclareceu muita coisa.

Foi necessário realizar uma atualização no arquivo de repositórios do debian `/etc/apt/sources.list` que ficou assim:

```
deb [trusted=yes] http://archive.debian.org/debian/ jessie main contrib non-free
deb-src [trusted=yes] http://archive.debian.org/debian/ jessie main contrib non-free
deb [trusted=yes] http://archive.debian.org/debian-security jessie/updates main contrib non-free
deb-src [trusted=yes] http://archive.debian.org/debian-security jessie/updates main contrib non-free
deb [trusted=yes] http://archive.debian.org/debian jessie-backports main contrib non-free
deb-src [trusted=yes] http://archive.debian.org/debian jessie-backports main contrib non-free
deb [trusted=yes] http://chip.jfpossibilities.com/chip/debian/repo jessie main
deb [trusted=yes] http://chip.jfpossibilities.com/chip/debian/pocketchip jessie main
```

Também foi necessário instalar a chave da NTC, debian e outras mais devido a mensagem de erro `W: GPG error: http://archive.debian.org jessie Release: The following signatures were invalid: KEYEXPIRED 1587841717`.

```bash
wget http://chip.jfpossibilities.com/chip/debian/NTC.pub
apt-key add - < NTC.pub
apt-get install debian-archive-keyring
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com 7638D0442B90D010
```

Depois disso consegui finalmente realizar um `apt upgrade`. Depois do upgrade deu certo:

```bash
apt-get install -f apt-transport-https
apt-get autoremove
```

Feito isso o conteúdo do arquivo `/etc/apt/sources.list.d/docker.list` ficou assim:

```
deb [arch=armhf signed-by=/etc/apt/keyrings/docker.gpg] http://download.docker.com/linux/debian   jessie stable
```

Com o docker rodando fiz a instalacao do compose:

```bash
curl -L https://github.com/docker/compose/releases/download/v2.21.0/docker-compose-linux-armv7 > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

Não quis me alongar muito nesse artigo pois se trata de uma necessidade muito específica e que gastei algumas horas para entender e resolver o problema. De modo que esse artigo é mais para documentar as etapas de modo que eu consiga me situar caso necessite refazer isso no futuro.

Se você chegou por aqui por também ter essa necessidade específica espero que esse artigo ajude a colocar uma luz no que está faltando no seu caso. Se desejar contratar minha consultoria basta entrar em contato, [Renato Monteiro Batista](http://renato.ovh).

Outros links que me ajudaram:
- [Reddit ChipCommunity](https://www.reddit.com/r/ChipCommunity/comments/16hdhwg/sourceslist/)
- [Flash CHIP](https://github.com/Thore-Krug/Flash-CHIP)
- [Install Docker on Debian 8 Jessie Server Via Official Repository](https://www.linuxbabe.com/linux-server/install-docker-on-debian-8-jessie-server)
- [https://download.docker.com/linux/debian/dists/jessie/pool/stable/armhf/](https://download.docker.com/linux/debian/dists/jessie/pool/stable/armhf/)
- [Releases do docker compose](https://github.com/docker/compose/releases/)