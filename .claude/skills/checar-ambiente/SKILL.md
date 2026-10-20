---
name: checar-ambiente
description: Confere se o ambiente de desenvolvimento está pronto (ferramentas, contas e conexões) e guia o usuário a resolver o que faltar, um item por vez. Use no começo do projeto, quando uma instalação ou um login falhar, ou antes de construir.
---

# Checar ambiente

O usuário é iniciante. Confira cada item rodando o comando de verificação você mesmo. Para cada item que faltar, explique em uma frase para que ele serve, dê a ação exata (um link ou um comando) e espere o usuário confirmar antes de verificar de novo.

## Itens

| # | Item | Verificação | Como resolver |
|---|---|---|---|
| 1 | Git | `git --version` | Mac: rodar `git --version` faz o sistema oferecer a instalação das "ferramentas de linha de comando"; aceite. Windows: https://git-scm.com/download/win |
| 2 | Node.js 20 ou mais novo | `node --version` | Instalar a versão LTS em https://nodejs.org |
| 3 | GitHub CLI | `gh --version` | Mac: instalador em https://cli.github.com. Windows: `winget install --id GitHub.cli` |
| 4 | Login no GitHub | `gh auth status` | O usuário roda `gh auth login` no terminal, escolhe GitHub.com, HTTPS e login pelo navegador |
| 5 | Projeto ligado ao GitHub | `git remote -v` mostra `github.com` | Pergunte o nome do projeto (sugira o nome da pasta) e se o repositório deve ser privado ou público. Depois rode `git init`, faça o primeiro commit com o kit e rode `gh repo create <nome> --private --source . --push` (ou `--public`). Mostre ao usuário o link do repositório criado |
| 6 | Label das issues | `gh label list` contém `ready-for-agent` | `gh label create ready-for-agent --description "Pronta para o agente"` |
| 7 | Supabase | `npx supabase projects list` | O usuário cria a conta em https://supabase.com (entrar com GitHub) e depois roda `npx supabase login` |
| 8 | Vercel | `npx vercel whoami` | O usuário cria a conta em https://vercel.com (entrar com GitHub) e depois roda `npx vercel login` |
| 9 | Chave da OpenRouter | `.env.local` tem `OPENROUTER_API_KEY` preenchida (confira só se existe) | O usuário cria a conta e a chave em https://openrouter.ai/keys. Crie o `.env.local` com as linhas `OPENROUTER_API_KEY=` e `OPENROUTER_MODEL=openrouter/free` (o modelo gratuito padrão, ver ADR-0001) e peça para ele colar a chave direto no arquivo. A conta e a chave são grátis e não pedem cartão |

Os comandos de login abrem o navegador e pedem interação. Peça para o usuário rodá-los no terminal dele, um de cada vez.

## Pronto quando

Os nove itens foram verificados por comando e aparecem como ✅ numa tabela final mostrada ao usuário.
