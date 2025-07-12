---
layout: post
title:  "Criando um novo blog usando o Jekyll Minima para GitHub Pages"
date: 2025-07-12 12:48 -0300
categories: [tech, tutorial]
tags: [jekyll, github-pages, blog, tutorial, minima]
author: "Renato Monteiro Batista"
---
Pré-requisitos
Git instalado: [git-scm.com](git-scm.com)

Ruby + DevKit: [ rubyinstaller.org](https://rubyinstaller.org)

Após instalar, abra o terminal e execute: `ridk install` e selecione as opções básicas.

Editor de código (ex: [Visual Studio Code](https://code.visualstudio.com/))

## Criar um novo repositório no GitHub

Vá para GitHub

Clique em “New” (Novo)

Nomeie o repositório como **username.github.io** (com seu nome de usuário)

### Clonar o repositório localmente

```bash
git clone https://github.com/renatomb/renatomb.github.io
cd renatomb.github.io
```

## Inicializar com Jekyll + tema Minima

```bash
gem install bundler jekyll
jekyll new . --force --skip-bundle
```

Isso criará a estrutura do blog.

### Configurar o tema Minima

Abra o arquivo Gemfile e substitua o conteúdo por:

```ruby
source "https://rubygems.org"
gem "jekyll", "~> 4.3.2"
gem "minima", "~> 2.5"
```

No config.yml, adicione:

```yaml
theme: minima
```

### Instalar dependências e rodar o blog localmente

```bash
bundle install
jekyll serve
```

Acesse http://localhost:4000 para ver seu blog rodando!

## Publicar no GitHub Pages

Faça commit e push:

```bash
git add .
git commit -m "Blog criado com Jekyll e Minima"
git push origin main
``` 

Vá até as configurações do repositório no GitHub

Em “Pages”, selecione a branch main e a pasta raiz / como origem

Seu blog estará em https://renatomb.github.io em alguns minutos!