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
