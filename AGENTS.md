# Como trabalhar neste projeto

Converse com o usuário sempre em português do Brasil, inclusive nas entrevistas (grill), nas especificações, nas issues e nos commits. O usuário é um empresário, não um programador. Explique cada passo técnico em uma frase simples antes de executá-lo.

## A stack já está decidida

Leia `docs/adr/0001-stack-padrao.md`. A stack é premissa do projeto. No grill, trate-a como decisão tomada e gaste as perguntas com o negócio.

## O método, na ordem

| Etapa | Comando | Pronto quando |
|---|---|---|
| Ambiente | `/checar-ambiente` | todos os itens do check-up estão ✅ e o projeto do Lovable, novo ou copiado de um que já existe, está ligado ao GitHub |
| Alinhar | `/grill-with-docs` | nenhuma decisão em aberto e `CONTEXT.md` atualizado |
| Especificar | `/to-spec` e depois `/to-tickets` | a spec e os tickets publicados como issues no GitHub |
| Construir | `/implement` | um ticket por conversa; ao fim de cada ticket, commit e push na `main`, e o resultado aparece no preview do Lovable |
| Expandir | o mesmo fluxo, a partir do `/grill-with-docs` | cada módulo novo nasce com sua própria spec e seus tickets |

Num projeto que já existe, leia o código, o `CONTEXT.md` e os ADRs antes do grill e pergunte só o que muda.

O usuário pode pausar o grill a qualquer momento e voltar depois. Quando ele voltar, ou perguntar o que fazer agora, descubra a etapa pelo estado do projeto (`CONTEXT.md` e `docs/adr/`, as issues com `gh issue list --state all` e o `git log`) e diga exatamente o próximo comando.

Se o usuário quiser o app com a cara da empresa, ele passa o site e a logo no grill. Veja `docs/agents/visual.md`.

## Lovable

O app roda no Lovable, e você escreve o código aqui. Antes de mexer em código, banco ou IA do app, leia `docs/agents/lovable.md`. Em resumo: código no computador e push na `main`; banco pelo SQL do conector do Lovable; o agente do Lovable só com autorização do usuário, porque gasta créditos.

## Chaves e senhas

O usuário não precisa colar nenhuma chave: o Lovable Cloud guarda as do banco e da IA. O `.env` do repositório tem só as chaves públicas do banco, criadas pelo Lovable. Nunca mostre o valor de uma chave na conversa.

## Agent skills

### Issue tracker

As issues ficam no GitHub deste repositório e são manipuladas com o `gh`. Veja `docs/agents/issue-tracker.md`.

### Triage labels

Os cinco papéis padrão (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). Veja `docs/agents/triage-labels.md`.

### Domain docs

Single-context: um `CONTEXT.md` e uma pasta `docs/adr/` na raiz. Veja `docs/agents/domain.md`.
