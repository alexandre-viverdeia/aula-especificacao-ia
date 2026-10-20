---
name: marca
description: Extrai a identidade visual da empresa a partir do site e da logo e grava o DESIGN.md, que guia todo o visual do app. Use quando o usuário passar o site ou a logo da empresa, ou pedir que o app tenha a cara da marca.
---

# Marca

O `DESIGN.md` é a fonte única do visual do app: cores, fontes, logo e tom de voz. Toda tela construída depois segue esse arquivo.

## Passos

1. **Pegue as duas entradas.** Peça o endereço do site e a logo (arquivo ou link). Sem logo, siga só com o site e registre isso.
2. **Leia o site como um designer.** Baixe o HTML e as folhas de estilo e procure:
   - as variáveis de cor em `:root` e as cores mais repetidas;
   - as fontes (links do Google Fonts, `@font-face`, `font-family`);
   - o `theme-color`, o favicon e a imagem de compartilhamento (`og:image`);
   - o tom de voz dos títulos e dos botões.
   Sites montados por JavaScript guardam isso nos arquivos `.css` e `.js` que o HTML carrega: abra esses arquivos também.
3. **Guarde a logo** em `public/brand/` (por exemplo, `public/brand/logo.png`).
4. **Escreva o `DESIGN.md`** na raiz, com:
   - **Paleta:** primária, fundo, superfície, texto, texto secundário, borda, sucesso, alerta e erro, cada uma com hexadecimal e de onde ela veio;
   - **Tipografia:** fonte de títulos, fonte de texto e como carregar cada uma;
   - **Forma:** raio dos cantos, sombras, espaçamento e o estilo geral em uma frase;
   - **Logo:** o caminho do arquivo e onde ela aparece (topo do app, landing page, favicon);
   - **Tom de voz:** três adjetivos e um exemplo de frase tirada do site;
   - **Tokens:** as variáveis CSS prontas para o Tailwind e o shadcn/ui (`--primary`, `--background`, `--foreground` e as demais).
5. **Mostre um resumo ao usuário** (as cores principais, as fontes e o tom de voz) e ajuste o que ele pedir.

## Pronto quando

O `DESIGN.md` existe, cada cor e cada fonte nele tem origem no site, na logo ou numa confirmação do usuário, e o usuário aprovou o resumo.
