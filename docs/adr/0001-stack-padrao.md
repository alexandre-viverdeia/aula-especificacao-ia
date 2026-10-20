# Stack padrão: Next.js + Supabase + Vercel + OpenRouter, versionado no GitHub

Todo projeto deste kit nasce com a mesma stack mínima, escolhida antes do grill para que a entrevista se concentre no negócio. Os critérios: é gratuita para começar, é usada por empresas de verdade, a IA conhece bem cada peça e as peças se conectam sem código de integração.

- **Next.js (App Router) com TypeScript**: o app inteiro, as telas e o servidor, num projeto só. É o formato nativo da Vercel.
- **Tailwind CSS e shadcn/ui**: componentes prontos, que recebem as cores e as fontes do `DESIGN.md`.
- **Supabase**: banco Postgres e login (Supabase Auth). O acesso aos dados é protegido por Row Level Security. As mudanças no banco entram como migrations versionadas no repositório.
- **Vercel**: hospedagem, ligada ao repositório do GitHub. Cada push na `main` publica sozinho.
- **OpenRouter, via AI SDK**: toda chamada de IA do app passa por uma chave só. O modelo fica numa variável de ambiente (`OPENROUTER_MODEL`), então trocar de modelo é mudar uma linha.
- **Vitest**: testes automatizados, que dão ao agente o retorno de que o código funciona (a skill `/tdd` depende disso).
- **GitHub**: histórico do código e issues (a spec e os tickets).

## Consequências

Qualquer peça nova, como e-mail ou WhatsApp, entra como módulo por cima desta base, com sua própria spec. Trocar uma das peças acima é uma decisão nova, registrada em um ADR novo.
