---
name: continuar
description: Descobre em que etapa do método o projeto está e leva o usuário ao próximo passo. Use quando o usuário voltar ao projeto depois de uma pausa, perguntar o que fazer agora ou disser que ficou para trás na aula.
---

# Continuar

O usuário parou em algum ponto do método (ambiente, grill, marca, spec, tickets, construção) e quer seguir. O estado do projeto mostra onde ele está: leia o estado, não pergunte.

## Passos

1. **Leia o estado do projeto:**
   - `CONTEXT.md` e `docs/adr/`: o que o grill já decidiu;
   - `DESIGN.md`: se a marca já foi aplicada;
   - `gh issue list --state all`: a spec e os tickets, abertos e fechados;
   - `git log --oneline -15` e `package.json`: o que já foi construído;
   - `docs/agents/lovable-projeto.md` e `git remote -v`: se o projeto do Lovable existe e está ligado ao GitHub.
2. **Encontre a primeira etapa incompleta**, nesta ordem:

   | Sinal | Próximo passo |
   |---|---|
   | ferramentas, contas ou o projeto do Lovable faltando | `/checar-ambiente` |
   | sem `CONTEXT.md`, ou grill com decisões em aberto | `/grill-with-docs`, retomando a partir do `CONTEXT.md` e das decisões em aberto |
   | sem `DESIGN.md` | `/marca` |
   | sem issue de spec | `/to-spec` |
   | spec sem tickets | `/to-tickets` |
   | tickets abertos | `/implement` no primeiro ticket sem bloqueio, numa conversa nova |
   | todos os tickets fechados | conferir o app no preview do Lovable, publicar e escolher o próximo módulo (`/grill-with-docs` de novo) |

3. **Explique ao usuário**, em linguagem simples: onde ele está, o que já está pronto e o comando exato do próximo passo.

Se o usuário pausou o grill no meio, a forma mais fiel de retomar é abrir a mesma conversa no app. Numa conversa nova, use o `CONTEXT.md` e os ADRs para não repetir perguntas já respondidas.

## Pronto quando

O usuário sabe em que etapa está e tem exatamente um próximo comando para rodar.
