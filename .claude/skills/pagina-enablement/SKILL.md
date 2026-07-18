---
name: pagina-enablement
description: >-
  Cria ou evolui páginas de enablement interativas no padrão do time — voz
  api4com (informal, sem "cara de Claude"), design system "sinal sobre tinta",
  componentes interativos (wizard travado, stepper, accordions) e publicação em
  GitHub Pages. Use quando o pedido for construir um guia/treinamento interno
  como página web ("monta uma página de enablement sobre X", "cria um guia
  interativo pro time sobre Y") ou ao atualizar a Central de Enablement.
---

# Página de Enablement — o método do time

Você está construindo ou evoluindo uma página de enablement interativa. Siga
ESTE método e ESTA voz. Não invente um formato do zero: o objetivo é que toda
página saia com a mesma identidade e sem "cara de Claude".

Arquivos de apoio (leia sob demanda, conforme a fase):
- [references/voz.md](references/voz.md) — como escrever. **Leia antes de redigir qualquer texto.**
- [references/metodo.md](references/metodo.md) — estrutura, componentes e a auditoria anti-perda.
- [references/publicar.md](references/publicar.md) — fluxo de publicação no GitHub Pages.
- [templates/base.html](templates/base.html) — esqueleto com o design system e os componentes prontos.

## Pare e pergunte (junte num checkpoint só)
- Público e formato ainda ambíguos.
- Onde publicar, qual marca e qual visibilidade — confirme ANTES de publicar (é o passo que sai pra fora).
Na dúvida entre perguntar e seguir num passo reversível, siga.

## O método (nesta ordem)
1. **Entender** — quem é o público (pode ser mais de um perfil) e qual a tarefa da página.
2. **Pesquisar a fonte certa** — nunca invente fato técnico. Instalação/produto/ferramenta → docs oficiais (WebFetch, agente `claude-code-guide`). Estatística/afirmação → fonte citável. Puxe exemplos REAIS do material do time (transcrições, repo, memórias) em vez de genéricos.
3. **Estruturar** — ver [references/metodo.md](references/metodo.md). Menos é mais: esconda profundidade em blocos que abrem (`<details>`). Uma seção = um objetivo.
4. **Escrever na voz** — ver [references/voz.md](references/voz.md). Esta é a etapa que tira a cara de Claude. Não pule.
5. **Interatividade real** — a pessoa faz algo pra avançar (marca passo, clica etapa, abre bloco). Reaproveite os componentes de [templates/base.html](templates/base.html).
6. **Auditar perdas** — ao reescrever ou enxugar, compare termo a termo com a versão anterior. Enxugar ≠ apagar. Receita de grep em [references/metodo.md](references/metodo.md). NUNCA perca contexto que o usuário corrigiu ao longo do caminho.
7. **Publicar** — ver [references/publicar.md](references/publicar.md). Prévia via Artifact + site no GitHub Pages. Confirme marca/visibilidade antes.

## Regras duras
- **Voz api4com sempre.** Sem "não é X, é Y"; sem títulos empilhados (rótulo + H2 + sub-H3 juntos); sem excesso de negrito e travessão; sem tagline de marketing.
- **Não reinvente o design.** Cores, tipografia e componentes vêm de [templates/base.html](templates/base.html).
- **Interativo > estático.** Se a pessoa só rola e lê, faltou interatividade.
- **Preserve o acumulado.** Cada correção do usuário é contexto que não se perde ao otimizar. Audite antes de publicar.
- **noindex por padrão** (conteúdo interno).
- **Fato técnico só de fonte oficial.** Na dúvida, diga que não sabe — não chute link nem versão.
