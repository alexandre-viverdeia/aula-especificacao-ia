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
| 4 | Login no GitHub | `gh auth status` | Rode `gh auth login --web -h github.com -p https` em segundo plano e leia a saída. Mostre ao usuário o código de uso único e o link https://github.com/login/device: ele abre o link, cola o código e autoriza. Quando ele confirmar, rode `gh auth setup-git` e verifique de novo |
| 5 | Projeto ligado ao GitHub | `git remote -v` mostra `github.com` | Pergunte o nome do projeto (sugira o nome da pasta) e se o repositório deve ser privado ou público. Depois rode `git init`, faça o primeiro commit com o kit e rode `gh repo create <nome> --private --source . --push` (ou `--public`). Mostre ao usuário o link do repositório criado |
| 6 | Label das issues | `gh label list` contém `ready-for-agent` | `gh label create ready-for-agent --description "Pronta para o agente"` |
| 7 | Conector do Supabase | As ferramentas do conector do Supabase estão disponíveis e listar as organizações funciona | O usuário cria a conta em https://supabase.com (entrar com GitHub). Depois, no app do Claude, abre Configurações → Conectores, conecta o Supabase e autoriza no navegador |
| 8 | Conector da Vercel | As ferramentas do conector da Vercel estão disponíveis e listar os times funciona | O usuário cria a conta em https://vercel.com (entrar com GitHub). Depois, no app do Claude, abre Configurações → Conectores, conecta a Vercel e autoriza no navegador |
| 9 | Chave da OpenRouter | `.env.local` tem `OPENROUTER_API_KEY` preenchida (confira só se existe) | O usuário cria a conta e a chave em https://openrouter.ai/keys. Crie o `.env.local` com as linhas `OPENROUTER_API_KEY=` e `OPENROUTER_MODEL=openrouter/free` (o modelo gratuito padrão, ver ADR-0001) e peça para ele colar a chave direto no arquivo. A conta e a chave são grátis e não pedem cartão |

Não peça para o usuário abrir o terminal: você roda os comandos e ele só clica nos links e autoriza.

Os conectores carregam no começo da conversa. Se o usuário acabou de conectar o Supabase ou a Vercel e as ferramentas não aparecem, peça para ele abrir uma conversa nova nesta pasta e rodar `/checar-ambiente` de novo; os itens que já estão prontos passam rápido. Não use as CLIs `supabase` e `vercel` para fazer login: o login delas não funciona quando é o agente que roda o comando.

Nesta etapa, não crie nada no Supabase nem na Vercel: os projetos são criados na construção. Nunca mexa em projetos que já existiam na conta sem perguntar.

**No Codex:** em vez dos conectores, adicione os servidores MCP do Supabase (`https://mcp.supabase.com/mcp`) e da Vercel (`https://mcp.vercel.com`) nas configurações de MCP do Codex e faça o login de cada um.

## Pronto quando

Os nove itens foram verificados por comando e aparecem como ✅ numa tabela final mostrada ao usuário.
