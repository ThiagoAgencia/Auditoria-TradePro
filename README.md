# Auditoria TradePro

Site interno da Agência Mult para acompanhar promotores, visitas e lojas
auditados via TradePro.

## Como abrir o site publicado

Depois de ativar o GitHub Pages (veja abaixo), o site fica disponível em:

```
https://thiagoagencia.github.io/Auditoria-TradePro/
```

## Estrutura

```
index.html          → o site inteiro (interface, cálculos, gráficos)
vendor/              → bibliotecas de terceiros usadas (leitura de Excel e gráficos),
                        guardadas aqui dentro pra não depender de nenhum serviço externo
data/                → criado automaticamente pelo site na primeira vez que alguém salvar dados
                        (um arquivo .json por distribuidora + um index.json)
```

## Como ativar o GitHub Pages

1. No repositório, vá em **Settings** → **Pages**.
2. Em "Source", escolha **Deploy from a branch**.
3. Em "Branch", escolha **main** e a pasta **/ (root)**.
4. Clique em **Save**. Em alguns minutos o link acima fica no ar.

## Como permitir que o site salve dados (token do GitHub)

O site em si é só leitura pra qualquer visitante. Pra **salvar** dados novos
(depois de subir um Relatório de Roteiro), quem estiver atualizando precisa
de um token pessoal do GitHub:

1. No GitHub, vá em **Settings** (do seu perfil, não do repositório) → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**.
2. Clique em **Generate new token**.
3. Em "Repository access", escolha **Only select repositories** e selecione **Auditoria-TradePro**.
4. Em "Permissions" → "Repository permissions", ache **Contents** e mude pra **Read and write**.
5. Gere o token e copie (só aparece uma vez).
6. No site, vá em **Atualizar Dados** → cole o token no campo indicado → **Salvar token neste navegador**.

O token fica guardado só no navegador de quem colou (localStorage), nunca é
enviado a ninguém além do próprio GitHub.

## Como atualizar os dados

1. Exporte o Relatório de Roteiro no TradePro (.xls ou .xlsx).
2. No site, vá em **Atualizar Dados**, digite o nome da distribuidora e suba o arquivo.
3. Confira o resumo que aparece ("X visitas lidas de Y promotores").
4. Clique em **Salvar no GitHub**.

Visitas de meses diferentes se somam automaticamente (não substitui dados
antigos) — o site identifica cada visita pela combinação
Colaborador + Loja + Data, então re-subir o mesmo arquivo não duplica nada.

## Flags de fotos suspeitas

Como o site não guarda as fotos em si (só dados), a aba "Fotos" mostra
contadores por loja com base num arquivo `.json` que o Claude gera depois de
revisar o álbum fotográfico, no formato:

```json
[
  {"colaborador": "Nome", "loja": "Nome da Loja", "data": "2026-08-10", "tipo": "tela"},
  {"colaborador": "Nome", "loja": "Nome da Loja", "data": "2026-08-11", "tipo": "preta"}
]
```

`tipo` pode ser `tela`, `preta`, `duplicada` ou `outro`.
