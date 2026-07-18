# Publicar (GitHub Pages)

A página é um único `index.html` estático, sem dependências externas
(CSP-safe: CSS e JS inline, nada de CDN, imagens como data URI).

## Prévia rápida
Publique via ferramenta **Artifact** pro usuário navegar antes de virar site.
O corpo do arquivo é escrito SEM `<head>` (a ferramenta embrulha).

## Virar site
1. Ao virar site, embrulhe o corpo com um `<head>` próprio:
   ```html
   <!doctype html><html lang="pt-BR"><head>
     <meta charset="utf-8">
     <meta name="viewport" content="width=device-width, initial-scale=1">
     <meta name="robots" content="noindex, nofollow">
     <title>...</title>
     <link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ctext y='.9em' font-size='90'%3E%F0%9F%93%A1%3C/text%3E%3C/svg%3E">
   </head><body>
   <!-- conteúdo -->
   </body></html>
   ```
2. Repositório novo + push (público é grátis; `noindex` mantém fora do Google; privado de verdade exige plano pago):
   ```bash
   gh repo create <nome> --public --source=. --remote=origin --push
   ```
3. Ligar o Pages:
   ```bash
   gh api -X POST repos/<owner>/<repo>/pages --input - <<< '{"source":{"branch":"main","path":"/"}}'
   ```
4. Esperar o build e conferir:
   ```bash
   gh api repos/<owner>/<repo>/pages/builds/latest --jq '.status'   # até "built"
   curl -s -o /dev/null -w "%{http_code}" https://<owner>.github.io/<repo>/   # até 200
   ```
5. Atualizar depois: editar `index.html`, commit, push → rebuilda sozinho no mesmo link.

## Cuidados (Windows / Git Bash)
- Commit sem depender de config global:
  `git -c user.name="<nome>" -c user.email="<email>" commit -m "..."`
- Confirme a branch antes de commitar (o repo pode ter várias): `git branch --show-current`.

## Confirmar antes de publicar (passo que sai pra fora)
- Marca correta no cabeçalho e rodapé.
- Visibilidade: público-não-listado (grátis, `noindex`) vs privado (plano pago) vs Notion (atrás do login do workspace).
- Rollback é fácil: `gh repo delete` ou desligar o Pages. O site some, o código fica.
