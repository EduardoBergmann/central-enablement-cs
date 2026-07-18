# Estrutura e componentes

## Princípios
- Uma seção = um objetivo. Menos é mais.
- Interativo > estático: a pessoa faz algo pra avançar.
- Profundidade escondida em `<details>` — a página abre curta.
- Um H2 por seção. Sem rótulo em cima.
- Tema claro/escuro via tokens CSS. `noindex` por padrão.

## Componentes (todos prontos em `templates/base.html`)
- **Seletor de trilha + dossiê** — 2 a 3 perfis. Ao clicar, o conteúdo abaixo **TROCA inteiro** pra falar com aquele perfil (trocar, não só destacar). Cada dossiê: foco + pontos com exemplo e link "aprofundar".
- **Wizard travado** — checklist onde o próximo passo só abre quando o anterior é marcado. Barra de progresso. Salva no `localStorage`. Use pra instalação / onboarding / qualquer sequência obrigatória.
- **Stepper** — etapas clicáveis (dots + voltar/próximo). Cada etapa revela conceito + analogia do dia a dia + o que pedir pro Claude. Use pra ensinar um fluxo (ex.: Git).
- **Accordion (`<details class="acc">`)** — esconde profundidade (técnicas, exemplos, troubleshooting). Nativo, acessível, sem JS.
- **Turnos "você diz → ele faz"** — duas colunas pra ensinar como pedir.
- **Cards / auto-item** — grades de exemplos e "tarefa manual → como automatizar".
- **Hero com onda (canvas)** — sinal de telecom, sutil, respeita `prefers-reduced-motion`.

## Fontes de conteúdo (não invente)
- Fato de ferramenta/produto → doc oficial (WebFetch; agente `claude-code-guide` pra Claude Code).
- Exemplos → material real do time (transcrições, repo, memórias). Genérico é o que mais soa a Claude.
- Cite a fonte no rodapé de cada seção que usa fato externo.

## Auditoria anti-perda (passo 6 — obrigatório ao reescrever)
Enxugar não pode apagar contexto que o usuário já corrigiu. Antes de publicar:
1. Liste os termos-chave do conteúdo acumulado (metáforas do time, exemplos reais, nomes próprios, decisões, correções).
2. `grep -ic` cada termo na versão NOVA vs na ANTIGA (a que está no ar).
3. Se algum termo caiu de ">0" pra "0", foi perda — restaure.
4. Contagem menor (dedup) é ok; ausência não é.

Receita:
```bash
for t in "tradutor de linguagem" "Bot Demanda CS" "estagiário" "churn"; do
  printf "%-28s novo=%s antigo=%s\n" "$t" \
    "$(grep -ic "$t" novo.html)" "$(grep -ic "$t" antigo.html)"
done
```

## Revisão ortográfica (parte b do passo 6)
Erro de português destrói a credibilidade do material. Antes de publicar, extraia o
texto visível (sem tags) e leia inteiro — não confie na leitura "por cima" do HTML.

Extrair o texto visível pra revisar:
```bash
perl -0777 -pe 's/<style.*?<\/style>//gs; s/<script.*?<\/script>//gs; s/<[^>]+>/ /g; s/&nbsp;/ /g; s/&gt;/>/g; s/&amp;/\&/g; s/[ \t]+/ /g;' pagina.html | grep -vE '^\s*$'
```
Ao ler, cace especialmente:
- **Concordância** plural/singular. Ex. real que escapou: "parece sete palavra difícil" → "parecem sete palavras difíceis".
- **Crase** (à/a), **acento** (vêm/vem, é/e), pontuação.
- O tique **"não é X, é Y"** (é erro de voz, não de ortografia, mas mata junto).
Um espaço antes de vírgula/ponto na extração costuma ser artefato de `<span>` — confira no HTML antes de "corrigir".

## Checklist antes de publicar
- [ ] Voz api4com aplicada (sem "não é X, é Y", sem títulos empilhados).
- [ ] Pelo menos um componente interativo por página.
- [ ] Auditoria anti-perda rodada (nenhum termo-chave zerado).
- [ ] **Texto visível lido de ponta a ponta — zero erro de português.**
- [ ] Marca e visibilidade confirmadas com o usuário.
- [ ] `noindex` no `<head>`. Tema claro/escuro funcionando.
