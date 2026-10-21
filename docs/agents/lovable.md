# Lovable

O app roda no Lovable: o projeto novo do Lovable é TanStack Start (React e TypeScript, Tailwind CSS e shadcn/ui), com o Lovable Cloud (banco Postgres e login) e o Lovable AI (a IA do app). Um projeto que já existe pode ter outra base, como React com Vite e funções em `supabase/functions/`: confira no `package.json` e siga o padrão que o projeto já usa. O código mora no repositório do GitHub ligado ao Lovable. O que você envia para a `main` aparece no editor do Lovable em segundos.

O nome, o id do projeto e o link do editor estão em `docs/agents/lovable-projeto.md`, criado pelo `/checar-ambiente`.

## Quem faz o quê

| Tarefa | Como | Crédito do Lovable |
|---|---|---|
| Código, telas, regras e testes | Você, no computador: commit e push na `main` | não gasta |
| Criar ou alterar tabelas e políticas de acesso | SQL pela ferramenta `query_database` do conector do Lovable | não gasta |
| Consultar ou inserir dados de teste | `query_database` | não gasta |
| Publicar o app | `deploy_project` do conector, ou o botão Publicar no editor | não gasta |
| Criar o projeto | `create_project`, uma vez, no `/checar-ambiente` | cerca de 0,4 |
| Copiar um projeto que já existe | `remix_project`, uma vez, no `/checar-ambiente` | confira no saldo do Lovable |
| O que nenhum caminho acima resolve | `send_message` para o agente do Lovable | gasta |

O plano gratuito do Lovable dá 5 créditos por dia. Antes de qualquer `send_message`, explique ao usuário por que não há outro caminho e peça a autorização dele.

## Mudanças no banco

1. Escreva o SQL (tabela, colunas, Row Level Security e políticas) e rode com `query_database`.
2. Salve o mesmo SQL em `supabase/migrations/<AAAAMMDDHHMMSS>_<descricao>.sql`, para ficar no histórico.
3. Atualize à mão `src/integrations/supabase/types.ts`. O Lovable não regenera esse arquivo quando o SQL vem de fora. Consulte `information_schema.columns` com `query_database` e siga o formato que já está no arquivo, com `Row`, `Insert` e `Update` para cada tabela.
4. Rode `npx tsc --noEmit` antes do commit.

Toda tabela nasce com Row Level Security ligada. O `query_database` roda no banco de verdade: não apague dados nem tabelas sem pedir.

## A IA do app (Lovable AI)

Chame o gateway do Lovable a partir de uma função de servidor: `createServerFn`, de `@tanstack/react-start`, no TanStack Start; uma função em `supabase/functions/`, chamada com `supabase.functions.invoke`, num projeto com Vite. Lá a chave vem de `Deno.env.get("LOVABLE_API_KEY")`. A chave `LOVABLE_API_KEY` já existe no servidor do Lovable Cloud: nunca a coloque no código nem na conversa.

```ts
const res = await fetch("https://ai.gateway.lovable.dev/v1/chat/completions", {
  method: "POST",
  headers: { Authorization: `Bearer ${process.env["LOVABLE_API_KEY"]}`, "Content-Type": "application/json" },
  body: JSON.stringify({ model: "google/gemini-2.5-flash", messages }),
});
```

No computador essa chave não existe. Faça a função devolver um erro claro quando ela faltar, cubra a lógica em volta com testes e confira a chamada real no preview do Lovable.

## No computador

- Instale as dependências com `npm install --no-package-lock`. O Lovable usa o `bun.lock`, e um `package-lock.json` não deve ir para o repositório.
- Antes de cada push, rode `npx tsc --noEmit` e `npm test`.
- O usuário confere o resultado no preview do editor do Lovable.
- Não reescreva o histórico que já foi enviado (force push, rebase ou amend de commits enviados): o Lovable perde o histórico do projeto.
- Não edite `src/routeTree.gen.ts`, que é gerado automaticamente.
