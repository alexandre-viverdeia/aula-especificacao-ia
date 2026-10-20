# Stack padrão: Next.js + Supabase + Vercel + OpenRouter, versionado no GitHub

Todo projeto deste kit nasce com a mesma stack mínima, escolhida antes do grill para que a entrevista se concentre no negócio. Os critérios: é gratuita para começar, é usada por empresas de verdade, a IA conhece bem cada peça e as peças se conectam sem código de integração.

- **Next.js (App Router) com TypeScript**: o app inteiro, as telas e o servidor, num projeto só. É o formato nativo da Vercel.
- **Tailwind CSS e shadcn/ui**: componentes prontos, que recebem as cores e as fontes do `DESIGN.md`.
- **Supabase**: banco Postgres e login (Supabase Auth). O acesso aos dados é protegido por Row Level Security. As mudanças no banco entram como migrations versionadas no repositório.
- **Vercel**: hospedagem, ligada ao repositório do GitHub. Cada push na `main` publica sozinho.
- **Conectores do Supabase e da Vercel**: o agente cria e configura os projetos pelos conectores do app do Claude, que o usuário liga com um clique. O login pelas CLIs `supabase` e `vercel` não funciona quando é o agente que roda o comando.
- **OpenRouter, via AI SDK**: toda chamada de IA do app passa por uma chave só, a do próprio usuário. O modelo fica numa variável de ambiente (`OPENROUTER_MODEL`), então trocar de modelo é mudar uma linha. O padrão é `openrouter/free`, que escolhe a cada chamada um modelo gratuito disponível e capaz de atender o pedido: custo zero, com limite de 50 chamadas por dia (1.000 depois de comprar 10 créditos na OpenRouter).
- **Vitest**: testes automatizados, que dão ao agente o retorno de que o código funciona (a skill `/tdd` depende disso).
- **GitHub**: histórico do código e issues (a spec e os tickets).

## O que fica para o grill

A stack diz por onde a IA passa, não qual modelo o produto usa. Pergunte no grill:

- quem escolhe o modelo: fixo na configuração, numa tela de Configurações do app, ou um modelo por tarefa;
- se dados reais de clientes podem ir para modelos gratuitos. Alguns provedores gratuitos podem usar o que recebem para treinar; com dados reais, o caminho é um modelo pago com o treino desligado nas configurações de privacidade da OpenRouter.

A chave nunca aparece numa tela do app: ela fica no `.env.local` e nas variáveis de ambiente da Vercel.

## Consequências

Qualquer peça nova, como e-mail ou WhatsApp, entra como módulo por cima desta base, com sua própria spec. Trocar uma das peças acima é uma decisão nova, registrada em um ADR novo.
