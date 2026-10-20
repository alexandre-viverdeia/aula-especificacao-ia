# Kit da aula: Como montar a especificação técnica de um projeto de IA

Este kit é o ponto de partida do seu projeto. Ele traz o método da aula pronto para usar: as skills que fazem a IA te entrevistar, transformar as respostas em especificação e tarefas e só então construir.

> **O método é do Matt Pocock.** As skills principais deste kit (`grill-with-docs`, `to-spec`, `to-tickets`, `implement` e as que elas usam por baixo) vêm do workflow que ele publica em [github.com/mattpocock/skills](https://github.com/mattpocock/skills). Nós selecionamos só as que o fluxo da aula usa, ajustamos para funcionarem no app do Claude e somamos três skills feitas para a aula. Quer entender o porquê de cada etapa? Veja a seção [Para se aprofundar](#para-se-aprofundar).

Você não precisa saber programar. Na maior parte do caminho, quem guia é a própria IA.

## 1. Crie as contas

| Conta | Para quê | Plano |
|---|---|---|
| [Claude](https://claude.ai) | O agente que constrói com você (Claude Code) | **Pro ou superior (pago)** |
| [GitHub](https://github.com/signup) | Guarda o histórico do projeto e as tarefas | Gratuito |
| [Supabase](https://supabase.com) | O banco de dados e o login do app. Use "Continue with GitHub" | Gratuito para começar |
| [Vercel](https://vercel.com/signup) | Coloca o app no ar. Use "Continue with GitHub" | Gratuito para começar |
| [OpenRouter](https://openrouter.ai) | A IA dentro do app, com vários modelos numa chave só | Gratuito com o `openrouter/free` (50 usos de IA por dia), sem cartão |

## 2. Instale o app do Claude

Baixe em https://claude.ai/download (Mac ou Windows) e faça login. Depois, em **Personalizar → Conectores** (*Customize → Connectors* no app em inglês), conecte o **Supabase** e a **Vercel**: é assim que a IA vai criar o banco e colocar o app no ar por você. O resto das instalações a IA vai te guiar no passo 4.

## 3. Baixe o kit e abra no Claude

1. Nesta página, clique em **Code → Download ZIP**.
2. Descompacte o arquivo. A pasta que aparece, `aula-especificacao-ia-main`, já é o seu projeto: só renomeie com o nome dele, por exemplo `crm-minha-empresa`, e deixe num lugar fácil, como Documentos. Não crie uma pasta antes nem mova os arquivos de dentro dela para outra: as pastas `.claude` e `.agents` ficam ocultas no Finder e ficariam para trás.
3. Abra o app do Claude, entre na aba **Code** e selecione essa pasta.

## 4. Rode o check-up do ambiente

Mande na conversa:

```
/checar-ambiente
```

A IA confere o que falta no seu computador (Git, Node.js, GitHub CLI), te ajuda a ligar as contas e cria o repositório do seu projeto no GitHub. Siga um item por vez até todos ficarem ✅.

## 5. Comece pelo grill

```
/grill-with-docs Quero o núcleo de um CRM para a minha empresa. Vendo [o quê] para [quem].
```

A IA vai te fazer perguntas em rodadas, cada uma com uma resposta recomendada. Responda com calma: é aqui que a especificação nasce. Se a aula andar mais rápido que você, pause o grill e volte depois. Nada se perde.

## Ficou para trás ou voltou outro dia?

```
/continuar
```

A IA olha o seu projeto, descobre em que etapa você parou e te diz o próximo passo.

## O método, do começo ao fim

| Etapa | Comando |
|---|---|
| Ambiente | `/checar-ambiente` |
| Alinhar | `/grill-with-docs` |
| Marca | `/marca`, com o site e a logo da sua empresa |
| Especificar | `/to-spec` e depois `/to-tickets` |
| Construir | `/implement`, um ticket por conversa |

## Usa o Codex?

Abra a mesma pasta no Codex e chame as skills com `$` em vez de `/`. Exemplo: `$grill-with-docs`. No lugar dos conectores, o `$checar-ambiente` te guia a ligar os servidores MCP do Supabase e da Vercel.

## As skills do kit

| Skill | Origem | Para quê |
|---|---|---|
| `checar-ambiente` | criada para a aula | Confere ferramentas e contas e cria o repositório no GitHub |
| `grill-with-docs` | Matt Pocock | A IA te entrevista até não sobrar dúvida |
| `marca` | criada para a aula | Lê o site e a logo e grava o visual do app |
| `to-spec` | Matt Pocock | Transforma a conversa numa especificação |
| `to-tickets` | Matt Pocock | Quebra a especificação em tickets pequenos, em ordem |
| `implement` | Matt Pocock | Constrói um ticket, com testes e revisão |
| `continuar` | criada para a aula | Descobre onde você parou e diz o próximo passo |
| `grilling`, `domain-modeling`, `tdd`, `code-review`, `codebase-design` | Matt Pocock | Rodam por baixo das skills acima |

## Para se aprofundar

- **[github.com/mattpocock/skills](https://github.com/mattpocock/skills):** o repositório original, com todas as skills do Matt. O README explica os quatro problemas que o método resolve: a IA não fazer o que você quer, falar demais, entregar código que não funciona e virar uma bola de lama.
- **[aihero.dev](https://www.aihero.dev):** o site e a newsletter do Matt sobre engenharia com IA.

## Créditos e licença

As skills marcadas como "Matt Pocock" são de autoria dele e estão sob licença MIT; o texto da licença está em `LICENSE-mattpocock-skills`. Para a aula, fizemos dois ajustes: elas vêm dentro do projeto e sem a trava `disable-model-invocation`, que faz o app desktop esconder essas skills. As skills `checar-ambiente`, `marca` e `continuar` foram criadas por Alexandre Axioma para esta aula.
