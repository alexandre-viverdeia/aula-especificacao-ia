# Como montar a especificação técnica de um projeto de IA

**Guia completo do fluxo de desenvolvimento**

Alexandre Axioma · Aula ao vivo G4 · outubro de 2026

---

## Como usar este guia

A aula tem três materiais, cada um com um papel:

| Material | Papel |
|---|---|
| **Slides** | Guiam a aula ao vivo: a sequência, os passos e o combinado. |
| **Este guia** | Explica o fluxo de desenvolvimento em detalhe, etapa por etapa. É o material para consultar depois. |
| **Kit de skills** | A pasta que efetivamente constrói o projeto com você, dentro do Claude Code ou do Codex. |

Este guia serve para duas leituras:

- **Para você:** leia uma vez de ponta a ponta para entender o fluxo inteiro. Depois, volte à etapa em que estiver.
- **Para o seu agente de IA:** entregue este arquivo ao Claude Code ou ao Codex e escreva "me guia". A última seção foi escrita para o agente: ele descobre em que etapa você parou e te leva ao próximo passo.

---

## 1. O problema: por que "faz um sistema pra mim" não funciona

Quando você pede para a IA construir um sistema sem especificar, ela preenche cada lacuna com um palpite. O resultado parece pronto, mas quebra no primeiro caso real, porque a IA decidiu sozinha, e em silêncio, tudo o que você não disse.

Um exemplo do CRM que construímos na aula: duas linhas da planilha com "Acme Ltda" e "ACME" são a mesma empresa? Um negócio pode existir sem empresa? O que acontece com um lead que ninguém chamou há sete dias? Se você não decide, a IA decide por você, e você só descobre depois.

**Especificar é tomar essas decisões antes do código, e deixá-las escritas.** Uma boa especificação responde: que problema estamos resolvendo, para quem, com quais regras e, tão importante quanto, o que fica de fora.

O fluxo deste guia vem do workflow de engenharia publicado pelo **Matt Pocock** ([github.com/mattpocock/skills](https://github.com/mattpocock/skills)). Ele organiza o trabalho com IA em torno de quatro falhas comuns:

| Falha | O que acontece | O que resolve |
|---|---|---|
| A IA não faz o que você quer | Você e a IA não estão alinhados sobre o que construir | O **grill**: a IA te entrevista antes de começar |
| A IA fala demais e se perde | Cada um usa uma palavra diferente para a mesma coisa | Um **glossário compartilhado** (`CONTEXT.md`) |
| O código não funciona | A IA constrói sem saber se o que fez está certo | **Testes** escritos antes do código |
| O projeto vira uma bola de lama | Cada mudança deixa o código mais difícil de mexer | **Tickets pequenos** e cuidado com o design do código |

---

## 2. A stack mínima

Uma empresa de software profissional não escolhe ferramentas do zero a cada projeto: ela tem uma stack padrão, e cada projeto nasce em cima dela. Fazemos o mesmo. A stack já vem decidida no kit (no arquivo `docs/adr/0001-stack-padrao.md`), e assim o grill gasta o seu tempo com o negócio, não com tecnologia.

Pense num restaurante:

| Peça | No restaurante | Para quê | Plano |
|---|---|---|---|
| **Claude Code** | O chef | Quem constrói, seguindo as skills do kit. Também funciona no Codex. | Claude Pro ou superior (pago) |
| **GitHub** | O caderno de receitas e as comandas | Guarda o histórico de tudo o que foi feito e as tarefas do projeto | Gratuito |
| **Supabase** | A despensa | O banco de dados e o login do app | Gratuito para começar |
| **Vercel** | O salão | Onde o app fica no ar para as pessoas usarem | Gratuito para começar |
| **OpenRouter** | Os fornecedores | A IA dentro do app, com vários modelos numa chave só | Modelos gratuitos para testar |

Por baixo, o app usa Next.js com TypeScript, Tailwind CSS e shadcn/ui para o visual, o AI SDK para falar com a OpenRouter e Vitest para os testes. Você não precisa dominar nenhuma dessas peças: o agente sabe usá-las, e a decisão está registrada no projeto.

---

## 3. O kit de skills

Uma **skill** é um conjunto de instruções que ensina o agente a fazer uma tarefa de um jeito específico, sempre igual. Em vez de você explicar toda vez como quer ser entrevistado ou como quer a especificação, a skill já carrega esse jeito.

O kit é uma pasta com as skills do fluxo já instaladas e configuradas. Você digita sete comandos; outras cinco skills rodam por baixo.

**Os comandos que você digita:**

| Comando | Origem | O que faz |
|---|---|---|
| `/checar-ambiente` | criada para a aula | Confere ferramentas e contas, guia o que faltar e cria o repositório do projeto no GitHub |
| `/grill-with-docs` | Matt Pocock | A IA te entrevista até não sobrar decisão em aberto e monta o glossário |
| `/marca` | criada para a aula | Lê o site e a logo da empresa e grava o visual do app no `DESIGN.md` |
| `/to-spec` | Matt Pocock | Transforma a conversa numa especificação, publicada como issue no GitHub |
| `/to-tickets` | Matt Pocock | Quebra a especificação em tickets pequenos, em ordem |
| `/implement` | Matt Pocock | Constrói um ticket, com testes e revisão de código |
| `/continuar` | criada para a aula | Lê o projeto, descobre onde você parou e diz o próximo passo |

**As que rodam por baixo** (todas do Matt Pocock): `grilling` (o jeito de entrevistar), `domain-modeling` (o glossário e as decisões), `tdd` (testes antes do código), `code-review` (a revisão antes de salvar) e `codebase-design` (o vocabulário para organizar o código).

**Usa o Codex?** Abra a mesma pasta no Codex e chame as skills com `$` em vez de `/`. Exemplo: `$grill-with-docs`.

---

## 4. O fluxo, etapa por etapa

### Etapa 0: configurar o ambiente

1. **Crie as contas:** Claude (Pro), GitHub, Supabase, Vercel e OpenRouter. Na Supabase e na Vercel, entre com "Continue with GitHub".
2. **Instale o app do Claude** em [claude.ai/download](https://claude.ai/download) e faça login.
3. **Baixe o kit:** na página do kit no GitHub, clique em **Code → Download ZIP**. Descompacte e dê à pasta o nome do seu projeto, por exemplo `crm-minha-empresa`.
4. **Abra a pasta no app do Claude**, na aba **Code**.
5. **Rode `/checar-ambiente`.** A IA confere Git, Node.js e GitHub CLI, ajuda nos logins, cria o repositório do projeto no seu GitHub e prepara o arquivo `.env.local` para a chave da OpenRouter.

**Pronto quando:** os nove itens do check-up aparecem como ✅.

### Etapa 1: alinhar com o grill

```
/grill-with-docs Quero o núcleo de um CRM para a minha empresa. Vendo [o quê] para [quem].
```

O grill é uma entrevista em rodadas. Em cada rodada, a IA faz as perguntas que já dá para responder e, para cada uma, sugere uma resposta (➡️). As suas respostas destravam as perguntas da rodada seguinte, até não sobrar nenhuma decisão em aberto.

**Como responder bem:**

- **Responda com casos reais.** "Ontem um lead chegou pelo Instagram e ninguém respondeu por três dias" vale mais que "quero organizar os leads".
- **A recomendação é um ponto de partida; a decisão é sua.** Quando ela não for a sua realidade, discorde e explique por quê.
- **"Não sei" é uma resposta válida.** Peça para a IA explicar as opções e o que muda com cada uma.
- **Decida o que fica de fora.** "Isso fica para depois" também é especificação, e protege o projeto de crescer sem controle.

**O que sai do grill:** o `CONTEXT.md`, o glossário do seu negócio (o que é um Lead, um Negócio, uma Empresa), e os ADRs em `docs/adr/`, com as decisões difíceis de reverter e o porquê de cada uma.

**Pausar e retomar:** se a aula andar mais rápido que você, pare de responder e acompanhe. Para voltar, abra a mesma conversa no app. Se ela tiver se perdido, rode `/continuar`: o agente usa o `CONTEXT.md` para retomar sem repetir perguntas.

**Pronto quando:** a IA não tem mais perguntas e você confirmou que ela entendeu o que deve ser construído.

### Etapa 2: aplicar a marca

```
/marca
```

Passe o site e a logo da sua empresa. A IA lê as cores, as fontes e o tom de voz do site e grava tudo no `DESIGN.md`. Toda tela construída depois segue esse arquivo, então o app já nasce com a cara da sua empresa.

**Pronto quando:** você aprovou o resumo de cores, fontes e tom de voz.

### Etapa 3: especificar e quebrar em tickets

Faça esta etapa **na mesma conversa do grill**: a spec e os tickets são construídos a partir de tudo o que foi conversado.

```
/to-spec
```

A especificação reúne, numa issue do GitHub: o problema, a solução do ponto de vista de quem usa, uma lista longa de histórias de usuário ("Como vendedor, quero ver quem chamar hoje, para não esquecer nenhum lead"), as decisões de implementação, o que será testado e o que fica fora do escopo.

```
/to-tickets
```

Os tickets são **fatias verticais**: cada um atravessa todas as camadas (banco, servidor, tela e testes) e entrega algo que você consegue ver funcionando. Cada ticket diz quais outros precisam estar prontos antes dele ("Blocked by"). A IA mostra a lista e pergunta se o tamanho e a ordem fazem sentido. Revise com calma: tickets bem cortados são o que faz a construção andar.

**Pronto quando:** a spec e os tickets estão publicados como issues no seu repositório do GitHub.

### Etapa 4: construir

```
/implement #3
```

**Um ticket por conversa.** Abra uma conversa nova para cada ticket: cada ticket tem tudo o que o agente precisa saber, e começar do zero evita que a conversa fique pesada e confusa.

Em cada ticket, o agente:

1. escreve um teste que falha, faz o código que passa no teste e repete, uma fatia por vez;
2. confere os tipos e roda os testes;
3. revisa o próprio código com `code-review`;
4. salva o trabalho com um commit no GitHub.

**O seu papel:** abrir o app no navegador e conferir se o ticket faz o que prometia. Se algo estiver diferente, descreva o que viu, não o que acha que é o código.

**As chaves:** a chave da OpenRouter e as do Supabase moram só no `.env.local`, que nunca vai para o GitHub. Cole as chaves direto nesse arquivo, nunca na conversa. Quando o projeto estiver ligado à Vercel, cada commit na `main` publica o app sozinho.

**Pronto quando:** todos os tickets estão fechados e o app está no ar na Vercel.

### Etapa 5: expandir o núcleo

O que você constrói primeiro é o **núcleo**: a parte que resolve a dor principal. Cada módulo novo, como o inbox do WhatsApp, a prospecção ativa ou as automações, passa pelo mesmo fluxo:

```
/grill-with-docs Quero que as mensagens do WhatsApp entrem no CRM.
```

Agora o grill conhece o projeto: ele lê o código, o `CONTEXT.md` e os ADRs, e pergunta só o que é novo ("mensagem de um número desconhecido vira lead novo?", "e se o contato já existir?"). Depois vêm `/to-spec`, `/to-tickets` e `/implement`, como antes.

---

## 5. O case da aula: o CRM da Viver de IA

| | |
|---|---|
| **A dor** | O dinheiro perdido não está nos leads que a empresa não tem. Está nos leads que ela já tem e esquece de chamar. |
| **Quanto custa** (números ilustrativos) | 80 leads por mês, 1 em cada 4 sem o segundo contato. Se 20% deles fechassem a R$ 4.000, são R$ 16.000 por mês na mesa. |
| **A promessa** | Nenhum lead esquecido: o CRM diz todo dia quem chamar, e a IA escreve o que falar. |

**O núcleo** que construímos:

- uma landing page ("Aplicação para a mentoria") cujo formulário joga o lead direto no funil;
- a importação de planilha, com a IA entendendo as colunas e apontando duplicados;
- empresas, contatos e negócios num funil em kanban;
- próxima ação obrigatória em todo negócio, e a tela "Hoje" com quem chamar;
- o alerta de negócio esfriando;
- o histórico de cada negócio;
- o painel do dono;
- a mensagem de follow-up escrita pela IA.

**Os próximos módulos**, que ficam de fora do núcleo: inbox do WhatsApp, direct do Instagram, prospecção ativa, automações, relatórios e integração com ERP.

---

## 6. Checklist

**Etapa 0, ambiente**

- [ ] As cinco contas criadas
- [ ] O check-up com os nove itens ✅
- [ ] O repositório do projeto criado no seu GitHub

**Etapas 1 a 3, especificar a solução**

- [ ] O grill respondido sobre o seu negócio
- [ ] O glossário (`CONTEXT.md`) e a marca (`DESIGN.md`) documentados
- [ ] A spec e os tickets publicados no GitHub

**Etapa 4, construir**

- [ ] O projeto ligado ao Supabase e à Vercel
- [ ] O primeiro ticket implementado e salvo no GitHub
- [ ] Todos os tickets fechados

**A solução final**

- [ ] A landing page no ar com a sua marca
- [ ] O lead do formulário caindo no funil
- [ ] O follow-up escrito pela IA

---

## 7. Glossário

| Termo | O que é |
|---|---|
| **Agente** | A IA que trabalha no seu computador: lê arquivos, roda comandos e escreve código. Aqui, o Claude Code ou o Codex. |
| **Skill** | Um conjunto de instruções que ensina o agente a fazer uma tarefa de um jeito específico. |
| **Repositório** | A pasta do projeto guardada no GitHub, com todo o histórico de mudanças. |
| **Commit** | Um ponto salvo no histórico. Se algo quebrar, dá para voltar a um commit anterior. |
| **Issue** | Uma tarefa registrada no GitHub. A spec e os tickets são issues. |
| **Spec** | A especificação: o documento que diz o que construir, para quem, com quais regras e o que fica de fora. |
| **Ticket** | Uma fatia pequena da spec, que dá para construir e conferir de uma vez. |
| **Grill** | A entrevista em que a IA te pergunta tudo o que precisa decidir antes de construir. |
| **`CONTEXT.md`** | O glossário do projeto: as palavras do seu negócio e o que cada uma significa. |
| **ADR** | Registro de uma decisão de arquitetura: o que foi decidido e por quê. Fica em `docs/adr/`. |
| **Deploy** | Colocar uma versão do app no ar. Na Vercel, acontece a cada commit na `main`. |
| **Migration** | Uma mudança na estrutura do banco de dados, salva como arquivo no projeto. |
| **`.env.local`** | O arquivo com as chaves secretas do projeto. Fica só no seu computador e nunca vai para o GitHub. |
| **Teste automatizado** | Um pequeno programa que confere se uma parte do app faz o que deveria. |

---

## 8. Problemas comuns

| Problema | O que fazer |
|---|---|
| "Essa skill não está instalada" | Confira se o app está aberto na pasta do projeto, a que tem o `AGENTS.md`. |
| O grill está demorando | É normal: é onde o valor está. Pause, acompanhe a aula e volte depois. |
| A IA quer pular etapas | Escreva: "siga o método do `AGENTS.md`, uma etapa por vez". |
| A conversa ficou longa e a IA se confunde | Abra uma conversa nova e rode `/continuar`. |
| Erro de chave ou de "unauthorized" | Confira se a chave está colada no `.env.local`, sem espaços. Gere uma chave nova se precisar. |
| O deploy falhou na Vercel | Peça ao agente: "leia o log do último deploy na Vercel e corrija o erro". |

---

## 9. Para se aprofundar

- **[github.com/mattpocock/skills](https://github.com/mattpocock/skills):** o repositório original do Matt Pocock, com todas as skills e a explicação de cada falha que o método resolve.
- **[aihero.dev](https://www.aihero.dev):** o site e a newsletter do Matt sobre engenharia com IA.
- **The Pragmatic Programmer** (David Thomas e Andrew Hunt) e **Domain-Driven Design** (Eric Evans): os livros de onde vêm várias ideias do método, como as fatias verticais e o glossário compartilhado.

---

## 10. Para o agente de IA que está lendo este guia

Você está ajudando um aluno da aula "Como montar a especificação técnica de um projeto de IA". Ele provavelmente é empresário, não programador. Converse em português simples, explique cada passo técnico em uma frase antes de executá-lo e deixe todas as decisões de negócio com ele.

1. **Confira se o projeto tem o kit:** procure o `AGENTS.md` e a pasta `.claude/skills` (ou `.agents/skills`, no Codex) na pasta aberta.
2. **Se o kit não estiver lá, instale-o:** baixe o repositório do kit (`git clone --depth 1 https://github.com/alexandre-viverdeia/aula-especificacao-ia` numa pasta temporária) e copie para a raiz do projeto as pastas `.claude`, `.agents` e `docs` e os arquivos `AGENTS.md`, `CLAUDE.md`, `.gitignore`, `README.md` e `GUIA-DA-AULA.md`. Preserve os arquivos que o aluno já tiver.
3. **Descubra a etapa:** rode `/continuar`. Ele lê o projeto e aponta a primeira etapa incompleta.
4. **Conduza uma etapa por vez,** na ordem da seção 4, usando a skill de cada etapa. O grill nunca é pulado: é nele que o aluno aprende a especificar.
5. **Encerre cada resposta** dizendo ao aluno onde ele está e qual é o próximo comando.
