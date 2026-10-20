# Projeto da aula: Como montar a especificação técnica de um projeto de IA

Converse com o usuário sempre em português do Brasil, inclusive nas entrevistas (grill), nas especificações, nas issues e nos commits. O usuário é um empresário, não um programador. Explique cada passo técnico em uma frase simples antes de executá-lo.

O método completo, etapa por etapa, está em `GUIA-DA-AULA.md`.

## A stack já está decidida

Leia `docs/adr/0001-stack-padrao.md`. A stack é premissa do projeto. No grill, trate-a como decisão tomada e gaste as perguntas com o negócio.

## O método, na ordem

| Etapa | Comando | Pronto quando |
|---|---|---|
| Ambiente | `/checar-ambiente` | todos os itens do check-up estão ✅ |
| Alinhar | `/grill-with-docs` | nenhuma decisão em aberto e `CONTEXT.md` atualizado |
| Marca | `/marca` | `DESIGN.md` criado a partir do site e da logo da empresa |
| Especificar | `/to-spec` e depois `/to-tickets` | a spec e os tickets publicados como issues no GitHub |
| Construir | `/implement` | um ticket por sessão, começando cada ticket numa conversa nova |
| Expandir | o mesmo fluxo, a partir do `/grill-with-docs` | cada módulo novo nasce com sua própria spec e seus tickets |

O usuário pode pausar o grill a qualquer momento para acompanhar a aula e voltar depois. Quando ele voltar, ou perguntar o que fazer agora, use `/continuar`.

## Supabase e Vercel

Fale com a Supabase e com a Vercel pelos conectores do app do Claude (no Codex, pelos servidores MCP de cada um). Toda mudança no banco aplicada pelo conector também é salva como arquivo em `supabase/migrations/`, para ficar no histórico do GitHub. Nunca mexa em projetos que já existiam na conta sem perguntar.

## Chaves e senhas

As chaves (OpenRouter, Supabase) moram só no arquivo `.env.local`, que já está no `.gitignore`. Peça para o usuário colar a chave direto nesse arquivo e nunca imprima o valor de uma chave na conversa.

## Agent skills

### Issue tracker

As issues ficam no GitHub deste repositório e são manipuladas com o `gh`. Veja `docs/agents/issue-tracker.md`.

### Triage labels

Os cinco papéis padrão (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). Veja `docs/agents/triage-labels.md`.

### Domain docs

Single-context: um `CONTEXT.md` e uma pasta `docs/adr/` na raiz. Veja `docs/agents/domain.md`.
