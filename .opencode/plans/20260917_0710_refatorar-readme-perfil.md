# Plano: Refatorar README.md do Perfil GitHub — tiagoeduardobr

> **Para workers agentic:** Usar `subagent-driven-development` (recomendado) ou `executing-plans` para implementar este plano tarefa por tarefa.
> Passos usam checkbox (`- [ ]`) para tracking.
> **Arquivo alvo:** `README.md` (único arquivo modificado neste plano).

---

## Contexto

O README.md (210 linhas) é o perfil público do GitHub de Tiago Eduardo Zimmermann. O usuário o considera **confuso** e pediu refatoração com 5 direções obrigatórias:

1. **Unificar hero** — remover duplicação: hero com typing SVG + badges (linhas 16-38) E H1 "Olá, eu sou o Tiago Eduardo Zimmermann!" + descrição (linhas 44-46). Deve haver UMA única introdução no topo.
2. **Remover stats duplicados** — card de GitHub Stats aparece DUAS vezes (linha 58 em "Sobre mim" e linha 93 em "GitHub Analytics"). Manter apenas na seção Analytics.
3. **Simplificar Tech Stack** — 5 subseções com ~20 badges. Enxugar para tecnologias principais com menos badges e mais foco.
4. **Remover seção Objetivo repetida** — "🎯 Objetivo" (linha 178) repete hero e "Sobre mim". Remover.
5. **Reordenar seções** — nova ordem: **Hero → Sobre mim → Projetos → Tech Stack → Analytics → Contato**.

## Objetivo

Produzir um README.md enxuto, sem duplicações, com ordem lógica de leitura (apresentação → quem sou → o que construí → com o que trabalho → métricas → contato), preservando todas as regras obrigatórias do projeto.

## Escopo

### Dentro
- Refatoração estrutural do `README.md` (remoções, simplificação, reordenação)
- Remoção temporária de Trophies e Activity Graph (com nota HTML comment para reativação futura)
- Preservação integral de: paleta de cores (HTML comment topo), hero, badges de visitas/seguidores, pins de projetos (deploy próprio), streak (herokuapp), contato, footer, badge "Feito com ❤", linha de stats para o sed do workflow

### Fora
- **NÃO** modificar `.github/workflows/update-stats.yml`
- **NÃO** reverter para URLs públicas genéricas (`github-readme-stats.vercel.app`)
- **NÃO** configurar tokens GITHUB_TOKEN1/2 no Vercel (fora do escopo deste repositório)
- **NÃO** alterar conteúdo dos pins de projetos, badges de contato ou textos do hero
- **NÃO** usar `<table>` (GitHub strips media queries — layout 100% full-width, cards empilham)

## Assumptions

1. O repositório `tiagoeduardobr/tiagoeduardobr` é o repositório especial de perfil — apenas `README.md` será modificado.
2. Trophies e Activity Graph serão **removidos temporariamente** com nota HTML comment (decisão recomendada pelo usuário — ambas as URLs atuais retornam erro: 500 e 402).
3. A simplificação da Tech Stack reduz de 20 para 10 badges, mantendo as tecnologias citadas no hero e no "Sobre mim" (Python, FastAPI, TypeScript, React, Pandas, Docker, SQL).
4. O formato da linha `Última atualização dos stats: DATA às HH:MM UTC` DEVE ser preservado exatamente para o `sed` do workflow `update-stats.yml` continuar funcionando.
5. A reordenação move o bloco "Projetos em Destaque" (linhas 112-174 atuais) para depois de "Sobre mim" e antes de "Tech Stack".

---

## Dependências

### Matriz de Dependências

| Task | Depende de | Premissa |
|------|-----------|----------|
| Task 1: Unificar hero | — | Região topo do arquivo |
| Task 2: Remover stats duplicado | — | Região "Sobre mim" |
| Task 3: Simplificar Tech Stack | — | Região "Tech Stack" |
| Task 4: Remover seção Objetivo | — | Região entre Projetos e Contato |
| Task 5: Remover Trophies/Graph | — | Região "GitHub Analytics" |
| Task 6: Reordenar seções | Tasks 1-5 | Reordenação só após remoções para evitar conflito de blocos |
| Task 7: Verificação final | Task 6 | Valida o arquivo completo |

> **Nota:** Tasks 1-5 são independentes em conteúdo (regiões distintas do arquivo), mas **devem ser executadas sequencialmente** — edições concorrentes no mesmo arquivo causariam conflito de linhas. A Task 6 (reordenação) depende de todas as anteriores.

### Pré-requisitos
- `README.md` no estado atual (210 linhas) — confirmado em 17/09/2026
- Workflow `.github/workflows/update-stats.yml` existente e funcional (não será tocado)

---

## Tasks

### Task 1: Unificar hero — remover H1 duplicado

**Arquivo:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

**Contexto:** O hero (linhas 16-38) já contém typing SVG (com "Olá!", "Tiago Eduardo Zimmermann", "Desenvolvedor Júnior"), badges de localização/disponibilidade/nível, contador de visitas/seguidores e descrição profissional. O H1 (linhas 44-46) repete nome, cargo e localização. Remover o H1 e manter o hero como única introdução.

**Passos:**
- [x] **Passo 1:** Remover o bloco duplicado: o separador `---` (linha 42), o `# Olá, eu sou o Tiago Eduardo Zimmermann!` (linha 44) e o parágrafo `Desenvolvedor Júnior em Blumenau/SC, buscando transformar ideias...` (linha 46).
- [x] **Passo 2:** Garantir que reste UM separador `---` entre o fim do hero (`<!-- ===== FIM HERO ===== -->`) e a seção `## 🚀 Sobre mim`.

**Verification:**
- Run: `grep -n "Olá, eu sou o Tiago" README.md`
- Expected: nenhum resultado (0 matches)
- Run: `grep -c "readme-typing-svg" README.md`
- Expected: `1` (hero único preservado)
- Run: `grep -n "FIM HERO" README.md`
- Expected: `1` ocorrência, seguida de `---` e depois `## 🚀 Sobre mim`

---

### Task 2: Remover stats duplicado da seção "Sobre mim"

**Arquivo:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

**Contexto:** O card de GitHub Stats aparece em "Sobre mim" (linhas 57-59) e em "GitHub Analytics" (linha 93). Manter apenas na seção Analytics.

**Passos:**
- [x] **Passo 1:** Remover o bloco `<p align="center">` com o card `github-readme-stats-tiagoeduardobr.vercel.app/api?username=...` localizado dentro da seção "Sobre mim" (após o último bullet `🤝 Aberto a conexões`).
- [x] **Passo 2:** Confirmar que a seção "Sobre mim" termina nos bullets, sem imagem de stats.

**Verification:**
- Run: `grep -c "github-readme-stats-tiagoeduardobr.vercel.app/api?" README.md`
- Expected: `1` (apenas o card da seção Analytics; o `/api/pin/` dos projetos não casa com este padrão `api?`)
- Run: `grep -n "Aberto a conexões" README.md`
- Expected: o bullet existe e é o último item da seção "Sobre mim" (sem `<p align="center">` de stats logo após)

---

### Task 3: Simplificar Tech Stack — de 20 para 10 badges

**Arquivo:** `README.md`
**Complexidade:** Média
**Dependências:** Nenhuma

**Contexto:** A seção "Tech Stack" (linhas 61-88) tem 5 subseções com 20 badges. Enxugar para as tecnologias principais (as citadas no hero e no "Sobre mim": Python, FastAPI, TypeScript, React, Pandas, Docker, SQL), mantendo as 5 subseções como estrutura.

**Passos:**
- [x] **Passo 1:** Na subseção `### 🎨 Frontend`, remover os badges de **HTML5**, **CSS3** e **JavaScript**. Manter: **TypeScript**, **React**, **React Native** (3 badges).
- [x] **Passo 2:** Na subseção `### 🐍 Backend`, remover o badge de **API REST**. Manter: **Python**, **FastAPI** (2 badges).
- [x] **Passo 3:** Na subseção `### 🗄️ Database`, manter **SQL** (1 badge, sem alteração).
- [x] **Passo 4:** Na subseção `### 📊 Data & AI`, remover o badge de **NumPy**. Manter: **Pandas**, **Jupyter Notebook** (2 badges).
- [x] **Passo 5:** Na subseção `### 🛠️ Tools & DevOps`, remover os badges de **Markdown** e **GitHub Actions**. Manter: **Git**, **Docker** (2 badges).

**Resultado esperado (10 badges):**
- Frontend: TypeScript, React, React Native
- Backend: Python, FastAPI
- Database: SQL
- Data & AI: Pandas, Jupyter Notebook
- Tools & DevOps: Git, Docker

**Verification:**
- Run: `grep -c "img.shields.io/badge" README.md | awk '{print $1}'` e comparar com a contagem da seção Tech Stack isolada
- Expected: na seção Tech Stack, exatamente **10** badges (`img.shields.io/badge`)
- Run: `grep -n "HTML5\|CSS3\|JavaScript-\|API_REST\|NumPy\|Markdown-\|GitHub_Actions" README.md`
- Expected: nenhum resultado na seção Tech Stack (0 matches dos badges removidos)

---

### Task 4: Remover seção "Objetivo" repetida

**Arquivo:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

**Contexto:** A seção `## 🎯 Objetivo` (linhas 176-178) repete o hero ("Desenvolvedor Júnior remoto", "Parecer Descritivo", "React Native") e o "Sobre mim". Remover completamente.

**Passos:**
- [x] **Passo 1:** Remover o bloco completo: `## 🎯 Objetivo` + o parágrafo `Busco oportunidades como **Desenvolvedor Júnior remoto**...`.
- [x] **Passo 2:** Garantir que a seção `## 📫 Contato` venha logo após o bloco de "Ver todos os repositórios" (fim de Projetos), sem resíduos da seção Objetivo.

**Verification:**
- Run: `grep -n "🎯 Objetivo" README.md`
- Expected: nenhum resultado (0 matches)
- Run: `grep -n "Ver%20todos%20os%20reposit" README.md`
- Expected: o badge "Ver todos os repositórios" existe e é seguido diretamente por `## 📫 Contato` (após a reordenação da Task 6, isso será validado novamente)

---

### Task 5: Remover Trophies e Activity Graph temporariamente (com nota HTML comment)

**Arquivo:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

**Contexto:** Na seção "GitHub Analytics" (linhas 90-110), dois cards estão quebrados:
- **Trophies** (linha 105): URL pública `github-profile-trophy.vercel.app` retorna **402**; deploy próprio retorna **500** (FUNCTION_INVOCATION_FAILED — tokens GITHUB_TOKEN1/2 não configurados no Vercel).
- **Activity Graph** (linha 109): instância pública `github-readme-activity-graph.vercel.app` retorna **402** (DEPLOYMENT_DISABLED).

**Decisão:** Remover temporariamente ambos, substituindo por HTML comment documentando como reativar. Manter Stats, Top Langs e Streak (funcionando).

**Passos:**
- [x] **Passo 1:** Remover o `<div align="center">` do card **Trophies** (linhas 104-106) e substituir por:
  ```html
  <!-- 🏆 GitHub Trophies — REMOVIDO TEMPORARIAMENTE (17/09/2026)
       URL pública (github-profile-trophy.vercel.app) retorna 402.
       Deploy próprio (github-profile-trophy-erunocarm-tiagoeduardobrs-projects.vercel.app) retorna 500
       até configurar GITHUB_TOKEN1 e GITHUB_TOKEN2 no Vercel.
       Reativar quando o deploy próprio responder HTTP 200:
       <img src="https://github-profile-trophy-erunocarm-tiagoeduardobrs-projects.vercel.app/?username=tiagoeduardobr&theme=onestar&no-frame=true&no-bg=true&row=2&column=3&margin-w=15&margin-h=15" width="100%" alt="GitHub Trophies"/>
  -->
  ```
- [x] **Passo 2:** Remover o `<div align="center">` do card **Activity Graph** (linhas 108-110) e substituir por:
  ```html
  <!-- 📊 Contribution Graph — REMOVIDO TEMPORARIAMENTE (17/09/2026)
       Instância pública (github-readme-activity-graph.vercel.app) retorna 402 DEPLOYMENT_DISABLED.
       Reativar quando houver instância própria funcionando:
       <img src="https://github-readme-activity-graph.vercel.app/graph?username=tiagoeduardobr&theme=github-dark&bg_color=0d1117&hide_border=true&point=58a6ff&color=58a6ff&line=3fb950&area=true" width="100%" alt="Contribution Graph"/>
  -->
  ```
- [x] **Passo 3:** Confirmar que a seção Analytics mantém exatamente 3 cards ativos: **Stats**, **Top Langs**, **Streak** (cada um em seu `<div align="center">`).

**Verification:**
- Run: `grep -n "github-profile-trophy\|github-readme-activity-graph" README.md`
- Expected: ocorrências apenas dentro de comentários HTML (`<!-- ... -->`), nenhuma como `<img src=...>` ativo
- Run: `grep -c "github-readme-streak-stats" README.md`
- Expected: `1` (streak preservado)
- Run: `grep -c "github-readme-stats-tiagoeduardobr.vercel.app/api?" README.md`
- Expected: `1` (stats) — top-langs usa `/api/top-langs/` e não casa com `api?`

---

### Task 6: Reordenar seções — Hero → Sobre mim → Projetos → Tech Stack → Analytics → Contato

**Arquivo:** `README.md`
**Complexidade:** Alta (movimentação de blocos)
**Dependências:** Tasks 1, 2, 3, 4, 5

**Contexto:** Após as remoções das Tasks 1-5, a ordem atual é: Hero → Sobre mim → Tech Stack → Analytics → Projetos → Contato → Footer. Mover o bloco "Projetos em Destaque" para depois de "Sobre mim" e antes de "Tech Stack".

**Passos:**
- [x] **Passo 1:** Identificar o bloco "Projetos em Destaque": do header `## 📌 Projetos em Destaque` até o badge "Ver todos os repositórios" (`<p align="center">` com `Ver%20todos%20os%20reposit`), inclusive.
- [x] **Passo 2:** Recortar esse bloco e inseri-lo entre o fim da seção "Sobre mim" (último bullet `🤝 Aberto a conexões`) e o header `## 🛠️ Tech Stack`.
- [x] **Passo 3:** Garantir separadores `---` consistentes entre as seções (padrão atual: `---` antes de cada `##`).
- [x] **Passo 4:** Validar a ordem final dos headers com `grep -n "^## "`.

**Ordem final esperada:**
```
## 🚀 Sobre mim
## 📌 Projetos em Destaque
## 🛠️ Tech Stack
## 📈 GitHub Analytics
## 📫 Contato
```

**Verification:**
- Run: `grep -n "^## " README.md`
- Expected (ordem exata):
  ```
  ## 🚀 Sobre mim
  ## 📌 Projetos em Destaque
  ## 🛠️ Tech Stack
  ## 📈 GitHub Analytics
  ## 📫 Contato
  ```
- Run: `grep -n "Ver%20todos%20os%20reposit" README.md` e `grep -n "## 🛠️ Tech Stack" README.md`
- Expected: linha do badge "Ver todos" é imediatamente anterior (com `---` entre) à linha de `## 🛠️ Tech Stack`

---

### Task 7: Verificação final — regras obrigatórias do projeto

**Arquivo:** `README.md`
**Complexidade:** Média
**Dependências:** Task 6

**Contexto:** Validar que nenhuma regra obrigatória foi quebrada durante a refatoração.

**Passos:**
- [x] **Passo 1:** Verificar que a linha de stats do workflow está preservada no formato exato que o `sed` espera:
  - Run: `grep -n "Última atualização dos stats:" README.md`
  - Expected: exatamente `1` ocorrência no formato `Última atualização dos stats: 17/08/2026 às 07:06 UTC` (a data atual pode variar — o que importa é o prefixo `Última atualização dos stats:` seguido de data e `UTC`, dentro de `<sub>...</sub>`)
- [x] **Passo 2:** Verificar que NENHUMA URL pública genérica foi reintroduzida:
  - Run: `grep -n "github-readme-stats.vercel.app" README.md`
  - Expected: nenhum resultado (0 matches) — todas as URLs de stats usam `github-readme-stats-tiagoeduardobr.vercel.app`
- [x] **Passo 3:** Verificar paleta de cores preservada no topo:
  - Run: `grep -n "Paleta de Cores" README.md`
  - Expected: `1` ocorrência no HTML comment das linhas 1-14
- [x] **Passo 4:** Verificar footer preservado:
  - Run: `grep -n "Feito%20com%20%E2%9D%A4%20por\|© 2026 Tiago Eduardo Zimmermann\|Gerado com ♥" README.md`
  - Expected: 3 ocorrências (badge "Feito com ❤", copyright, GitHub Actions)
- [x] **Passo 5:** Verificar pins de projetos preservados (4 pins + badge "Ver todos"):
  - Run: `grep -c "api/pin/" README.md`
  - Expected: `4`
- [x] **Passo 6:** Verificar contato preservado:
  - Run: `grep -c "img.shields.io/badge/GitHub-100000\|img.shields.io/badge/LinkedIn-0077B5\|img.shields.io/badge/Email-D14836" README.md`
  - Expected: `3`
- [x] **Passo 7:** Verificar que não há `<table>` no arquivo:
  - Run: `grep -c "<table>" README.md`
  - Expected: `0`
- [x] **Passo 8:** Verificar contagem final de linhas (deve ser menor que 210, estimativa 160-180):
  - Run: `wc -l README.md`
  - Expected: entre 150 e 190 linhas (arquivo enxuto, sem duplicações)
- [x] **Passo 9:** Verificar que o hero é a única introdução e que não há seções órfãs:
  - Run: `grep -n "^# \|^## " README.md`
  - Expected: `#` (H1) não deve existir; `##` na ordem: Sobre mim, Projetos em Destaque, Tech Stack, GitHub Analytics, Contato

**Verification final (consolidada):**
- Run: `grep -n "^## " README.md && grep -c "img.shields.io/badge" README.md && wc -l README.md`
- Expected: ordem correta das 5 seções; contagem total de badges consistente; arquivo entre 150-190 linhas

---

## Checkpoints

### Checkpoint 1: Hero unificado e stats sem duplicação (após Tasks 1-2)
- Verificar: `grep -n "Olá, eu sou o Tiago" README.md` → 0; `grep -c "github-readme-stats-tiagoeduardobr.vercel.app/api?" README.md` → 1
- Validação: ler visualmente as primeiras ~60 linhas do README — deve haver 1 introdução (hero) e "Sobre mim" sem card de stats

### Checkpoint 2: Tech Stack enxuta, Objetivo removido, Analytics limpo (após Tasks 3-5)
- Verificar: contagem de badges da Tech Stack = 10; `grep -n "🎯 Objetivo"` → 0; trophies/graph apenas em comentários HTML
- Validação: ler visualmente as seções Tech Stack e Analytics — sem badges removidos, sem cards quebrados

### Checkpoint 3: Ordem correta das seções (após Task 6)
- Verificar: `grep -n "^## " README.md` → Sobre mim, Projetos em Destaque, Tech Stack, GitHub Analytics, Contato (nesta ordem)
- Validação: ler o README completo de ponta a ponta — fluxo de leitura lógico e sem duplicações

### Checkpoint Final: Todas as tasks concluídas (após Task 7)
- Verificar: todos os passos da Task 7 passam (sed format, sem URLs públicas, paleta, footer, pins, contato, sem `<table>`, contagem de linhas)
- Validação: rodar a suíte completa de verificações da Task 7 e confirmar todos os Expected

---

## Riscos

| Risco | Probabilidade | Impacto | Mitigação |
|-------|--------------|---------|-----------|
| Quebrar o formato da linha de stats que o `sed` do workflow `update-stats.yml` espera | Baixa | Alto | Task 7 Passo 1 valida o formato exato `Última atualização dos stats:` antes de concluir |
| Reintroduzir URLs públicas genéricas (`github-readme-stats.vercel.app`) durante a reescrita | Baixa | Alto | Task 7 Passo 2 faz grep e exige 0 matches; regra documentada no Escopo/Fora |
| Perder conteúdo durante a movimentação de blocos (ex: badge "Ver todos os repositórios", pins) | Média | Médio | Task 7 Passos 5-6 validam contagem de pins (4) e badges de contato (3); Checkpoint 3 exige leitura completa |
| Usuário quiser reativar Trophies/Graph e não saber como | Média | Baixo | HTML comments das Tasks 5 documentam URLs e condição de reativação (HTTP 200) |
| Confusão de linhas ao editar o mesmo arquivo em tasks sequenciais | Média | Médio | Tasks 1-5 executadas sequencialmente; localização por conteúdo (grep), não por número de linha |

---

## Checklist Final de Aceitação

- [x] Hero é a ÚNICA introdução do perfil (sem H1 duplicado)
- [x] Card de GitHub Stats aparece apenas na seção Analytics (1 ocorrência de `/api?`)
- [x] Tech Stack com exatamente 10 badges (TypeScript, React, React Native, Python, FastAPI, SQL, Pandas, Jupyter, Git, Docker)
- [x] Seção "🎯 Objetivo" completamente removida
- [x] Trophies e Activity Graph removidos temporariamente com nota HTML comment (reativação documentada)
- [x] Ordem das seções: Hero → Sobre mim → Projetos → Tech Stack → Analytics → Contato
- [x] Formato `Última atualização dos stats: DATA às HH:MM UTC` preservado (sed do workflow continua funcionando)
- [x] Nenhuma URL pública genérica (`github-readme-stats.vercel.app`) presente
- [x] Paleta de cores (HTML comment topo) preservada
- [x] Footer preservado: badge "Feito com ❤", copyright © 2026, "Gerado com ♥ por GitHub Actions"
- [x] 4 pins de projetos + badge "Ver todos os repositórios" preservados
- [x] Contato preservado: GitHub, LinkedIn, Email (3 badges)
- [x] Sem `<table>` no arquivo (layout 100% full-width)
- [x] Arquivo final entre 150-190 linhas (enxuto vs. 210 originais)

---

## Feature List (tracking estruturado)

```json
{
  "features": [
    {
      "id": 1,
      "name": "Unificar hero (remover H1 duplicado)",
      "status": "done",
      "acceptance": [
        "Given o README atual com hero + H1 duplicado",
        "When o H1 e sua descrição são removidos",
        "Then existe UMA única introdução (hero) e grep por 'Olá, eu sou o Tiago' retorna 0"
      ]
    },
    {
      "id": 2,
      "name": "Remover stats duplicado de Sobre mim",
      "status": "done",
      "acceptance": [
        "Given o card de GitHub Stats em Sobre mim e em Analytics",
        "When o card de Sobre mim é removido",
        "Then grep por '/api?' retorna 1 (apenas Analytics)"
      ]
    },
    {
      "id": 3,
      "name": "Simplificar Tech Stack para 10 badges",
      "status": "done",
      "acceptance": [
        "Given 5 subseções com 20 badges",
        "When badges HTML5, CSS3, JavaScript, API REST, NumPy, Markdown, GitHub Actions são removidos",
        "Then a seção Tech Stack tem exatamente 10 badges"
      ]
    },
    {
      "id": 4,
      "name": "Remover seção Objetivo",
      "status": "done",
      "acceptance": [
        "Given a seção 🎯 Objetivo repetindo hero e Sobre mim",
        "When a seção é removida",
        "Then grep por '🎯 Objetivo' retorna 0"
      ]
    },
    {
      "id": 5,
      "name": "Remover Trophies e Activity Graph temporariamente",
      "status": "done",
      "acceptance": [
        "Given Trophies (500) e Activity Graph (402) quebrados",
        "When ambos são substituídos por HTML comment com nota de reativação",
        "Then nenhum <img> ativo de trophy/graph existe e streak/stats/top-langs permanecem"
      ]
    },
    {
      "id": 6,
      "name": "Reordenar seções",
      "status": "done",
      "acceptance": [
        "Given a ordem atual Hero → Sobre mim → Tech Stack → Analytics → Projetos → Contato",
        "When o bloco Projetos é movido para depois de Sobre mim",
        "Then a ordem final é Hero → Sobre mim → Projetos → Tech Stack → Analytics → Contato"
      ]
    },
    {
      "id": 7,
      "name": "Verificação final das regras obrigatórias",
      "status": "done",
      "acceptance": [
        "Given o README refatorado",
        "When a Task 7 é executada",
        "Then sed format preservado, sem URLs públicas, paleta/footer/pins/contato intactos, sem <table>, 150-190 linhas"
      ]
    }
  ]
}
```

---

*Plano criado em 17/09/2026 às 07:10 UTC pelo Task Planner Agent — baseado nas 5 direções de refatoração escolhidas pelo usuário e no estado dos endpoints testado em 17/09/2026.*
