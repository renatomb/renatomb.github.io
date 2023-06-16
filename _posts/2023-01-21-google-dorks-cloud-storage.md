---
layout: post
title:  "Pesquisas google para encontrar dados senssíveis em cloud storage"
date:   2023-01-21 14:40:00 -0300
tags: [google, dorks, segurança da informação, cloud storage]
author: "Renato Monteiro Batista"
---
Lista de *dorks* para encontrar dados sensíveis de alvos potenciais armazenados de maneira desprotegida em cloud storage e que foram indexados pelo Google, todos os resultados são públicos e podem ser acessados sem a necessidade de autenticação. Esses alvos podem ser explorados para fins de engenharia social, phishing, ataques de força bruta, etc.

## Exemplos de pesquisas

- `site:dropbox.com filetype:pdf`
- `site:http://s3.amazonaws.com "target[.]com"`
- `site:http://blob.core.windows.net "target[.]com"`
- `site:http://googleapis.com "target[.]com"`
- `site:http://drive.google.com "target[.]com"`
