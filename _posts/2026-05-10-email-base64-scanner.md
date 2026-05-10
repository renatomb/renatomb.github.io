---
layout: post
title:  "Filtrando e-mails com conteúdo codificado em Base64 utilizando o email-base64-scanner"
date:   2026-05-10 00:31:08 -0300
categories: [tech, tools]
tags: [e-mail, email, base64, scanner, filter, email-filter, email-base64-scanner, tool, cli, linha de comando, dovecot, cpanel, maildir]
author: "Renato Monteiro Batista"
---
# Filtrando e-mails com conteúdo codificado em Base64

Muita gente que trabalha com análise de e-mails ou segurança acaba esbarrando em mensagens que trazem partes importantes codificadas em Base64. Isso é bem comum em e-mails com HTML, anexos ou até tentativas de phishing.

O problema é que analisar esses e-mails manualmente dá trabalho. Por isso criei uma ferramenta simples para automatizar esse processo.

## O que é o email-base64-scanner

O [email-base64-scanner](https://github.com/renatomb/email-base64-scanner) é um script em Python que varre arquivos de e-mail, decodifica os blocos em Base64 e permite filtrar as mensagens com base em padrões que você definir.

Ele é especialmente útil quando você precisa:

- Encontrar e-mails que contenham domínios ou palavras específicas
- Analisar conteúdo que está escondido dentro de Base64
- Mover automaticamente e-mails suspeitos para outra pasta

## Como funciona

O script percorre todos os arquivos de um diretório, identifica os blocos com `Content-Transfer-Encoding: base64`, decodifica o conteúdo e verifica se existe algum dos padrões que você cadastrou no arquivo `filtrar-emails.txt`.

Se encontrar algum padrão, ele move o arquivo para o diretório de destino.

## Instalação e uso

Clone o repositório:

```bash
git clone https://github.com/renatomb/email-base64-scanner.git
cd email-base64-scanner
```

O uso básico é bem simples:

```bash
python3 email_filter.py /caminho/dos/emails /caminho/dos/emails-filtrados
```

### Principais opções

- `--dry-run`: Executa sem mover nenhum arquivo (bom para testar)
- `--show-preview`: Mostra um pedaço do conteúdo decodificado
- `--show-matched`: Exibe quais padrões foram encontrados
- `--verbose`: Mostra mais detalhes durante o processamento

Exemplo com algumas opções:

```bash
python3 email_filter.py --dry-run --show-matched --verbose /var/mail/inbox /var/mail/suspeitos
```

## Configurando os padrões

Os padrões são definidos no arquivo `filtrar-emails.txt`. Basta colocar um padrão por linha:

```txt
# Comentários começam com #
.malware-domain.com
.seu-dominio-suspeito.com
palavra-chave
```

O script busca esses padrões tanto no texto normal quanto no conteúdo decodificado do Base64.

## Exemplo prático

Suponha que você queira encontrar e-mails que contenham o domínio `malicious.example.com` dentro de partes codificadas:

1. Adicione o domínio no arquivo `filtrar-emails.txt`
2. Execute o script apontando para sua caixa de entrada
3. Os e-mails que baterem com o padrão serão movidos automaticamente

## Considerações

O script foi feito para ser simples e direto. Ele não é um antivírus completo, mas cumpre bem o papel de filtrar e-mails com base em padrões específicos dentro de conteúdo codificado.

Se você trabalha com análise de e-mails, triagem de caixas de entrada ou segurança, pode ser uma ferramenta útil para automatizar parte do trabalho.

O repositório está disponível em:  
[https://github.com/renatomb/email-base64-scanner](https://github.com/renatomb/email-base64-scanner)

Se usar e quiser dar alguma sugestão ou relatar algum problema, é só abrir uma issue lá.
