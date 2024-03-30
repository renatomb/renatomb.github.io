---
layout: post
title:  "Como acessar a Wikipedia, Stack Overflow, WikiHow e outros sites Kiwix de maneira offline sem internet usando o Docker"
date: 2024-03-30 10:30 -0300
categories: [tech, dicas, offline]
tags: [kiwix, wikipedia, stackoverflow, wikihow, serverfault, offline, download, internet, off-line, offline browsing, offline access, offline content, offline knowledge, offline information, offline resources, offline web, offline web browsing, offline web access, offline web content, offline web knowledge, offline web information, offline web resources, docker]
author: "Renato Monteiro Batista"
---
Qualquer dia aleatório você vai se encontrar sem acesso a internet, os motivos para isso podem ser vários, tais como:

- Viagem para um local sem cobertura de internet ou com internet muito lenta e não confiável
- Mudança de residência e atraso na instalação do serviço de internet
- Problemas técnicos com sua operadora de internet
- Acabou seu pacote de dados ou você não pode pagar o preço cobrado
- Estar em um local com internet bloqueada ou censurada
- Estar em um local com internet limitada, como em um avião ou em um cruzeiro
- Você gosta de estar preparado para qualquer situação apoacalíptica

Independentemente do motivo, há diversos sites de referência que você pode acessar de maneira offline sem internet, graças ao projeto Kiwix. Dentre esses sites posso citar a Wikipedia, Stack Overflow, WikiHow, ServerFault, entre outros.

## O que é o Kiwix

O Kiwix é um software que permite baixar e acessa-los sites de maneira offline, sem a necessidade de conexão com a internet. Ele é uma excelente ferramenta para quem precisa de acesso a informações de qualidade, mas não pode contar com uma conexão estável. Mas será necessário um pouco de espaço em disco para armazenar os arquivos baixados. A wikipedia em português, por exemplo, tem hoje (2024) cerca de 15GB de dados.

A instalação do Kiwix é bem simples, ele disponibiliza versões para Windows, MacOS, Linux, Android e iOS. Para baixar o software e os arquivos de dados dos sites que você deseja acessar offline, acesse o site oficial do [Kiwix](https://kiwix.org/en/applications/).

## Usando o Kiwix na versão docker em um HD externo

Mas nesse artigo vou detalhar o uso do Kiwix em um HD externo usando o docker. O uso do docker é interessante para quem não quer instalar o software diretamente no sistema operacional ou para quem quer usar o Kiwix em um HD externo e acessar de qualquer computador.

Para usar o Kiwix no docker é necessário ter a imagem `ghcr.io/kiwix/kiwix-serve` que atualmente está na sua versão 3.7.0. Para baixar a imagem execute o comando:

```bash
docker pull ghcr.io/kiwix/kiwix-serve:3.7.0
```

Mas lembre-se, você vai estar sem internet, então vamos salvar a imagem no disco (HD externo) para conseguir importar a imagem em outro computador caso necessário. Para salvar a imagem no disco execute o comando:

```bash
docker save -o kiwix-serve_3.7.0.tar ghcr.io/kiwix/kiwix-serve:3.7.0
```

Também é interessante baixar o [instalador do Docker](https://www.docker.com/products/docker-desktop/) para todos os sistemas operacionais onde você eventualmente vai estar usando esse disco.

Agora, para rodar o kiwix usando o docker vou criar um arquivo `docker-compose.yml` com o seguinte conteúdo:

```yaml
version: '3'
services:
  kiwix-serve:
    image: ghcr.io/kiwix/kiwix-serve:3.7.0
    volumes:
      - .:/data
    ports:
      - 8666:8080
    command: '*.zim'
```

Esse arquivo vai criar um container chamado `kiwix-serve` que vai servir todos os arquivos `.zim` que estiverem no diretório atual, em um webserver na porta `8666` do computador host.

## Onde baixar sites completos para acessar offline no formato `.zim`

Uma boa coleção de sites completos em formato `.zim` pode ser encontrada no [Kiwix Library](https://library.kiwix.org). Lá você vai encontrar sites como a Wikipedia, Stack Overflow, WikiHow, ServerFault, entre outros, alguns deles com diversas opções de idiomas. Baixe os arquivos `.zim` que você deseja acessar offline e coloque-os no mesmo diretório onde você criou o arquivo `docker-compose.yml`.

## Executando o container e acessando o conteúdo baixado de maneira offline

Para executar o container com o Kiwix execute o comando:

```bash
docker-compose up -d
```

Depois basta acessar, usando qualquer navegador, o endereço `http://localhost:8666` para acessar o Kiwix.
