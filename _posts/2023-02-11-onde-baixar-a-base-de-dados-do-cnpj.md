---
layout: post
title:  "Onde baixar a base de dados de CNPJ da Receita Federal"
date:   2023-02-11 12:19:00 -0300
author: "Renato Monteiro Batista"
---
Mensalmente o [Ministério da Economia divulga no portal dados abertos o conjunto de dados do CNPJ](https://dados.gov.br/dados/conjuntos-dados/cadastro-nacional-da-pessoa-jurdica---cnpj), que contém informações sobre as empresas brasileiras e pode ser baixado em formato CSV ou JSON.

Todos os downloads estão disponíveis para serem baixados via HTTP através do endereço [https://dadosabertos.rfb.gov.br/CNPJ/](https://dadosabertos.rfb.gov.br/CNPJ/)

Também é possível fazer o download acessando diretamente o IP do servidor no endereço [http://200.152.38.155/CNPJ/](http://200.152.38.155/CNPJ/)

## Fazendo um mirror da base de dados do CNPJ usando o wget

```bash
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent http://200.152.38.155/CNPJ/
```

## Repositórios no Github para trabalhar com o banco de dados de empresas da Receita Federal

Publiquei dois repositórios no github para tratamento dos dados dessa base de dados disponibilizada pela Receita Federal, são eles:

* [importar_cnpj](https://github.com/renatomb/importar_cnpj) se propõe a realizar a leitura dos dados e importa-los diretamente em um banco de dados mysql usando o `LOAD DATA LOCAL INFILE` e um [script python para tratar os dados da tabela Estabelecimentos](https://github.com/renatomb/importar_cnpj/blob/main/importar_estabe.py).
* [cnpj2sql](https://github.com/renatomb/cnpj2sql) é um projeto similar, mas feito em PHP, que se propõe a converter os arquivos `CSV` em arquivos `.sql` para importação direta em qualquer banco de dados MySQL. Além disso nele eu proponho uma estrutura diferente do banco de dados usando inteiros para os campos numéricos, o que reduziu consideravelmente o tamanho ocupado e o tempo de pesquisa no banco de dados.