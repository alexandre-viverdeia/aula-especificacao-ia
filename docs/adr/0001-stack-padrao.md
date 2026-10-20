# Stack padrão: Lovable + Claude Code, versionado no GitHub

Todo projeto deste kit nasce com a mesma stack mínima, escolhida antes do grill para que a entrevista se concentre no negócio. Os critérios: é gratuita para começar, pede poucas contas, a IA conhece bem cada peça e o usuário não precisa configurar servidor nem banco.

- **Lovable**: hospeda o app e gera o projeto inicial, em TanStack Start com React e TypeScript, Tailwind CSS e shadcn/ui.
- **Lovable Cloud**: banco Postgres e login. O acesso aos dados é protegido por Row Level Security. As mudanças no banco são feitas por SQL e salvas em `supabase/migrations/`.
- **Lovable AI**: a IA dentro do app, pelo gateway do Lovable, sem chave para o usuário configurar.
- **Claude Code**: escreve o código no computador, com as skills do kit, e envia para o GitHub; o Lovable recebe sozinho. O agente do Lovable só entra quando não há outro caminho, porque gasta créditos. Os detalhes estão em `docs/agents/lovable.md`.
- **GitHub**: o repositório ligado ao Lovable, que garante que o código é do usuário e não fica preso no Lovable, e as issues com a spec e os tickets.
- **Vitest**: testes automatizados, que já vêm no projeto do Lovable e dão ao agente o retorno de que o código funciona (a skill `/tdd` depende disso).

## O que fica para o grill

A stack diz onde o app roda, não como o produto usa a IA. Pergunte no grill:

- quem escolhe o modelo de IA: fixo no código, numa tela de Configurações do app, ou um modelo por tarefa;
- o que o app faz quando a IA falha ou quando o crédito de IA do mês acaba.

## Consequências

Qualquer peça nova, como e-mail ou WhatsApp, entra como módulo por cima desta base, com sua própria spec. Trocar uma das peças acima é uma decisão nova, registrada em um ADR novo.
