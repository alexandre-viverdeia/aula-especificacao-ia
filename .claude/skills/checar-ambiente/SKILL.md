---
name: checar-ambiente
description: Confere se o ambiente de desenvolvimento está pronto (ferramentas, contas e conexões), cria o projeto no Lovable e liga a pasta do kit a ele, guiando o usuário no que faltar, um item por vez. Use no começo do projeto, quando uma instalação ou um login falhar, ou antes de construir.
---

# Checar ambiente

O usuário é iniciante. Confira os itens na ordem, rodando a verificação você mesmo. Para cada item que faltar, explique em uma frase para que ele serve, faça o que dá para fazer por ele e dê a ação exata do que só ele pode fazer (um link ou um clique). Programas que faltam, você mesmo baixa e abre o instalador: o usuário só clica em Instalar e digita a senha do computador. Se faltarem vários, abra os instaladores todos de uma vez. Espere o usuário confirmar antes de verificar de novo. Não peça para o usuário abrir o terminal: você roda os comandos e ele só clica nos links e autoriza.

## Itens

| # | Item | Verificação | Como resolver |
|---|---|---|---|
| 1 | Git | `git --version` | Mac: veja "Instalar o Git no Mac". Windows: `winget install --id Git.Git -e --source winget` |
| 2 | Node.js 20.19 ou mais novo | `node --version` | Mac: descubra a versão LTS mais recente em https://nodejs.org/dist/index.json (o primeiro item com `lts` preenchido), baixe `https://nodejs.org/dist/<versão>/node-<versão>.pkg` para a pasta Downloads e abra com `open`. Windows: `winget install --id OpenJS.NodeJS.LTS -e --source winget` |
| 3 | GitHub CLI | `gh --version` | Mac: pegue o link do arquivo `gh_<versão>_macOS_universal.pkg` em https://api.github.com/repos/cli/cli/releases/latest, baixe para a pasta Downloads e abra com `open`. Windows: `winget install --id GitHub.cli -e --source winget` |
| 4 | Login no GitHub | `gh auth status` | Rode `gh auth login --web -h github.com -p https` em segundo plano e leia a saída. Mostre ao usuário o código de uso único e o link https://github.com/login/device: ele abre o link, cola o código e autoriza. Quando ele confirmar, rode `gh auth setup-git` e verifique de novo |
| 5 | Conector do Lovable | As ferramentas do conector do Lovable estão disponíveis e `list_workspaces` funciona | O usuário cria a conta em https://lovable.dev. Depois, no app do Claude, abre Personalizar → Conectores (Customize → Connectors, no app em inglês), conecta o Lovable e autoriza no navegador |
| 6 | Projeto no Lovable | `docs/agents/lovable-projeto.md` existe e `get_project` com o id dele funciona | Veja "Criar o projeto no Lovable" |
| 7 | Projeto ligado ao GitHub | `git remote -v` mostra o repositório que o Lovable criou | Veja "Ligar o GitHub e trazer o kit para o projeto" |
| 8 | Dependências e testes | `npm test` passa | `npm install --no-package-lock` e rode `npm test` de novo |
| 9 | Label das issues | `gh label list` contém `ready-for-agent` | `gh label create ready-for-agent --description "Pronta para o agente"` |

Os conectores carregam no começo da conversa. Se o usuário acabou de conectar o Lovable e as ferramentas não aparecem, peça para ele abrir uma conversa nova nesta pasta e rodar `/checar-ambiente` de novo; os itens que já estão prontos passam rápido.

## Instalar o Git no Mac

No Mac, o Git vem nas ferramentas de linha de comando da Apple, que chegam pelo atualizador do macOS. Instale em segundo plano, porque leva alguns minutos:

1. Rode `touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress` e depois `softwareupdate --list`.
2. Escolha o label "Command Line Tools for Xcode <versão>" com a versão igual à do macOS (`sw_vers -productVersion`) ou a mais próxima abaixo dela. Nunca uma versão maior que a do macOS.
3. Instale com a senha pedida numa janela do macOS:

   ```
   osascript -e 'do shell script "softwareupdate -i \"<label>\" && rm -f /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress" with administrator privileges'
   ```

Avise o usuário antes: vai abrir uma janela do macOS pedindo a senha do computador. Se esse caminho falhar, rode `xcode-select --install`, que abre a janela padrão da Apple; ela exige uns 25 GB livres no disco.

## Criar o projeto no Lovable

1. Pergunte o nome do projeto e sugira o nome da pasta.
2. Se `list_workspaces` trouxer mais de um workspace, pergunte em qual criar.
3. Avise que criar o projeto gasta cerca de 0,4 crédito do Lovable, uma vez só, e que o resto do fluxo quase não gasta. Com a confirmação, rode `create_project` com `wait: true` e a mensagem: "Projeto <nome>. Crie só uma página inicial simples com o nome do projeto. Não crie mais nada."
4. Ative o banco com `enable_database`, que não gasta crédito.
5. Crie `docs/agents/lovable-projeto.md` com o nome do projeto, o id, o workspace e o link do editor.

## Ligar o GitHub e trazer o kit para o projeto

1. Peça para o usuário abrir o link do editor e ligar o GitHub: o ícone do GitHub ou Settings → GitHub → Connect, escolhendo a conta dele. O Lovable cria um repositório privado com o código do app.
2. Encontre o repositório com `gh repo list --limit 5 --json name,url,createdAt` e confirme com o usuário.
3. Traga o código do Lovable para esta pasta sem sobrescrever os arquivos do kit:

   ```
   git clone <url do repositório> .lovable-tmp
   cp -Rn .lovable-tmp/. .
   ```

4. Se `.lovable-tmp/AGENTS.md` tiver um bloco entre `<!-- LOVABLE:BEGIN -->` e `<!-- LOVABLE:END -->`, copie esse bloco para o topo do `AGENTS.md` do kit. Depois apague a pasta `.lovable-tmp`.
5. Rode `npm install --no-package-lock` e `npm test`.
6. Faça um commit com o kit ("Kit da aula") e `git push origin main`. Explique ao usuário que o Lovable recebe o envio em segundos.

## Pronto quando

Os nove itens foram verificados e aparecem como ✅ numa tabela final, com o link do editor do Lovable e o do repositório no GitHub.

**No Codex:** em vez do conector, adicione o servidor MCP do Lovable (`https://mcp.lovable.dev`) nas configurações de MCP do Codex e faça o login.
