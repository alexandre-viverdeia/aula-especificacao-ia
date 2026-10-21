# Visual do app

Quando o usuário quiser que o app tenha a cara da empresa, ele passa o site e a logo, normalmente na primeira rodada do grill. Registre isso como decisão (no `CONTEXT.md` ou num ADR) e aplique no primeiro ticket que tiver telas:

1. **Leia o site como um designer.** Baixe o HTML e as folhas de estilo e procure as variáveis de cor em `:root` e as cores mais repetidas, as fontes (Google Fonts, `@font-face`, `font-family`), o `theme-color`, o favicon e o tom de voz dos títulos e dos botões. Sites montados por JavaScript guardam isso nos arquivos `.css` e `.js` que o HTML carrega.
2. **Guarde a logo** em `public/brand/`.
3. **Escreva o `DESIGN.md`** na raiz, com a paleta (cada cor com hexadecimal e de onde veio), a tipografia, a forma (cantos, sombras, espaçamento), a logo e onde ela aparece, o tom de voz e os tokens CSS para o Tailwind e o shadcn/ui (`--primary`, `--background`, `--foreground` e os demais).
4. **Mostre um resumo ao usuário** (cores principais, fontes e tom de voz) e ajuste o que ele pedir.

Toda tela construída depois segue o `DESIGN.md`.
