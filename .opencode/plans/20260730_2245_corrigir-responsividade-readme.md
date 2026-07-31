# Plano: Correção de Responsividade Mobile — README do Perfil GitHub (v3)

> **Para workers agentic:** Usar `subagent-driven-development` (recomendado) ou `executing-plans` para implementar este plano tarefa por tarefa.
> Passos usam checkbox (`- [ ]`) para tracking. Marcar `- [x]` + timestamp ao concluir cada passo.

**Objetivo:** Corrigir a responsividade do README.md do perfil GitHub no mobile, eliminando todas as tabelas de layout e garantindo que todos os cards de stats e projetos empilhem em full-width (`width="100%"`).

**Arquitetura:** O GitHub remove media queries/CSS de READMEs renderizados, então a única abordagem viável é empilhar todo o conteúdo em full-width usando apenas markdown puro, `<div>` e `<p align="center">` — sem `<table>` para layout. O markup de cada card é preservado (mesmas URLs, mesmas cores da paleta dark mode); apenas a estrutura de layout muda.

**Tech Stack:** Markdown, HTML inline (README.md), GitHub Actions (workflow de stats existente), github-readme-stats (deploy próprio no Vercel), Shields.io, Streak/Trophy/Activity Graph.

**Stack detectada:** Repositório de perfil GitHub (README.md). Nenhuma stack de aplicação detectada. Skills carregadas: `spec-driven-development`, `executing-plans`, `writing-plans`, `frontend-complete`.

---

## Contexto e Decisões de Planejamento

### Problema
O README atual usa 3 `<table>` para layout. Em mobile, tabelas com `<td width="60%">`/`<td width="40%">` (Sobre mim) e `<td width="50%">` (grid 2x2 de projetos) não empilham de forma confiável — o GitHub não permite media queries para corrigir.

### Decisões do planner (para revisão)
1. **Wrapper `<a>` do GitHub Analytics (linhas 112-117): REMOVER inteiramente.** A spec recomenda remover (mais simples); os 2 cards passam a ser blocos independentes com `width="100%"`. Evita área de toque gigante e link para repositório de terceiros envolvendo o card inteiro no mobile.
2. **Tabela do "Projeto Principal" (linhas 135-157): converter para `<div align="center">`.** A spec (Task 3) cobre apenas o grid de "Demais Projetos" (159-194), mas o critério de aceitação nº 1 exige "nenhuma `<table>` usada para layout". A tabela do destaque é single-column full-width (sem problema de mobile), porém viola o critério literalmente. Conversão incluída como subtask 3b — de baixo risco, preservando todo o conteúdo.
3. **Separador `---` da linha 27: REMOVER.** Sem os badges de paleta (16-25), o `---` fica órfão entre o comentário HTML da paleta e o HERO — renderizaria uma linha horizontal solta no topo do perfil.
4. **URLs custom do Vercel: PRESERVAR obrigatoriamente.** O commit `815af18` trocou todas as URLs de stats para `https://github-readme-stats-tiagoeduardobr.vercel.app/...`. Nenhuma edição deve reverter para `github-readme-stats.vercel.app` (genérico).
5. **Seção rodapé (linhas 220-236): NÃO TOCAR.** O workflow `.github/workflows/update-stats.yml` faz `sed` na linha "Última atualização dos stats:" — qualquer mudança na estrutura dessa linha quebra a automação.

---

## Premissas / Assumptions

1. A única stack é Markdown + HTML estático; não há testes automatizados — a verificação é feita via `grep` (integridade estrutural) e preview visual no GitHub (mobile).
2. Todas as URLs e cores atuais do README (paleta dark `#0d1117`, `#161b22`, `#58a6ff`, `#c9d1d9`, `#3fb950`) devem permanecer inalteradas — apenas a estrutura de layout muda.
3. As 4 descrições dos projetos em destaque e os 4 links de repositório devem ser preservados exatamente.
4. O comentário HTML da paleta (linhas 1-14) deve ser mantido (documenta a paleta no código-fonte sem poluir o visual).
5. A marcação do GitHub permite `<div>`, `<p>`, `<sub>`, `<br/>`, `<a>` e `<img width="100%">` — todos já usados no README atual.
6. Mudanças são feitas em um único arquivo (`README.md`); recomenda-se aplicar as tasks de cima para baixo no arquivo para diffs limpos.

---

## Escopo

### Dentro
- Substituir as 3 tabelas de layout por markdown/`<div>`/`<p>` full-width
- `width="100%"` em todos os cards de stats (stats, top langs, streak, trophies, activity graph)
- Cards de stats do GitHub Analytics empilhados (um por linha), sem `height="180em"`
- 4 projetos em destaque um por linha (full-width), sem grid 2x2
- Remover os 8 badges de paleta + separador `---` órfão; manter o comentário HTML da paleta
- Preservar deploy próprio do github-readme-stats no Vercel (commit `815af18`)

### Fora
- Não serão alteradas cores, textos, links ou URLs de badges existentes
- Não será alterado `.github/workflows/update-stats.yml` nem a linha de "Última atualização" do rodapé
- Não serão adicionadas media queries, CSS customizado ou JavaScript
- Não serão alteradas seções Hero, Tech Stack, Objetivo, Contato e rodapé

---

## Tasks

### Task 1: Corrigir seção "Sobre mim" (linhas 63-79)

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

Substituir a tabela `<td width="60%">` + `<td width="40%">` por bullets em markdown puro seguidos do stats card full-width centralizado.

- [x] **Passo 1: Substituir a tabela de "Sobre mim" por bullets + stats card full-width** – Concluído em 31/07/2026:08:10

  De: `<table>` com 2 colunas (linhas 63-79).
  Para:

  ```markdown
  ## 🚀 Sobre mim

  - 🔍 **Buscando oportunidade remota** — Desenvolvedor Júnior em transição, focado em construir projetos práticos e entregar valor real
  - 🚀 **Projeto Principal** — Construindo o [**Parecer Descritivo**](https://parecer-descritivo.onrender.com), app web com FastAPI + IA Generativa para professores da Educação Infantil
  - 📱 **React Native** — Estudando desenvolvimento mobile para expandir atuação como desenvolvedor
  - 🎓 **Formação** — Cursando Análise e Desenvolvimento de Sistemas, com aprendizado contínuo em Dados e IA
  - 🐍 **Stack Principal** — Python, FastAPI, TypeScript, React, Pandas, Docker, SQL
  - 🤝 **Aberto a conexões** — Buscando networking com devs, startups e empresas com cultura remota

  <p align="center">
    <img src="https://github-readme-stats-tiagoeduardobr.vercel.app/api?username=tiagoeduardobr&show_icons=true&theme=github_dark&hide_border=true&count_private=true&bg_color=0d1117&icon_color=58a6ff&text_color=c9d1d9&title_color=58a6ff" width="100%" alt="GitHub Stats"/>
  </p>
  ```

  > **Nota:** Manter exatamente a URL custom do Vercel (`github-readme-stats-tiagoeduardobr.vercel.app`) e os parâmetros atuais (`show_icons`, `theme=github_dark`, cores da paleta). Não usar o host genérico.

- [x] **Passo 2: Verificar que não sobrou resquício da tabela** – Concluído em 31/07/2026:08:10

  Run: `grep -n "width=\"60%\"\|width=\"40%\"" README.md`
  Expected: sem output (`width="60%"`/`width="40%"` não aparecem em nenhum lugar).

**Critério de aceitação:** Seção "Sobre mim" com os 6 bullets em markdown puro e stats card `width="100%"` centralizado abaixo; nenhuma tabela; URLs e textos idênticos ao original.

---

### Task 2: Corrigir seção "GitHub Analytics" (linhas 110-129)

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

Empilhar Stats e Top Langs (hoje lado a lado com `height="180em"` dentro de um `<a>` wrapper) em linhas próprias com `width="100%"`. Streak, Trophies e Activity Graph já têm `width="100%"` — manter intactos.

- [x] **Passo 1: Substituir o bloco Stats + Top Langs (wrapper `<a>` removido)** – Concluído em 31/07/2026:08:19

  De: `<div align="center">` > `<a href="https://github.com/anuraghazra/github-readme-stats">` com 2 `<img height="180em">` (linhas 112-117).
  Para:

  ```markdown
  ## 📈 GitHub Analytics

  <div align="center">
    <img src="https://github-readme-stats-tiagoeduardobr.vercel.app/api?username=tiagoeduardobr&show_icons=true&theme=github_dark&hide_border=true&count_private=true&bg_color=0d1117&icon_color=58a6ff&text_color=c9d1d9&title_color=58a6ff" width="100%" alt="GitHub Stats"/>
  </div>

  <div align="center">
    <img src="https://github-readme-stats-tiagoeduardobr.vercel.app/api/top-langs/?username=tiagoeduardobr&layout=compact&langs_count=6&theme=github_dark&hide_border=true&bg_color=0d1117&text_color=c9d1d9&title_color=58a6ff" width="100%" alt="Top Languages"/>
  </div>
  ```

  > **Decisão do planner:** o wrapper `<a href="https://github.com/anuraghazra/github-readme-stats">` foi **removido** (recomendação da spec). `height="180em"` removido dos dois cards; `width="100%"` adicionado.

- [x] **Passo 2: Confirmar que Streak, Trophies e Activity Graph permanecem inalterados** – Concluído em 31/07/2026:08:19

  Os blocos das linhas 119-129 já usam `width="100%"` — não editar:

  ```markdown
  <div align="center">
    <img src="https://github-readme-streak-stats.herokuapp.com/?user=tiagoeduardobr&theme=github-dark-blue&hide_border=true&background=0d1117&stroke=58a6ff&ring=58a6ff&fire=3fb950&currStreakLabel=58a6ff" width="100%" alt="GitHub Streak"/>
  </div>

  <div align="center">
    <img src="https://github-profile-trophy.vercel.app/?username=tiagoeduardobr&theme=onestar&no-frame=true&no-bg=true&row=2&column=3&margin-w=15&margin-h=15" width="100%" alt="GitHub Trophies"/>
  </div>

  <div align="center">
    <img src="https://github-readme-activity-graph.vercel.app/graph?username=tiagoeduardobr&theme=github-dark&bg_color=0d1117&hide_border=true&point=58a6ff&color=58a6ff&line=3fb950&area=true" width="100%" alt="Contribution Graph"/>
  </div>
  ```

- [x] **Passo 3: Verificar remoção do wrapper e do height fixo** – Concluído em 31/07/2026:08:19

  Run: `grep -n "anuraghazra" README.md && grep -n "height=\"180em\"" README.md`
  Expected: ambos os comandos sem output.

**Critério de aceitação:** 5 cards de stats todos com `width="100%"`, cada um em seu próprio `<div align="center">`; nenhum `height="180em"`; nenhum wrapper `<a>`; URLs custom do Vercel preservadas.

---

### Task 3: Corrigir seção "Projetos em Destaque" (linhas 131-194)

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Nenhuma

Transformar o grid 2x2 de "Demais Projetos" em 4 blocos full-width (um por linha) e converter a tabela do "Projeto Principal" em `<div>` (decisão do planner para cumprir o critério de aceitação nº 1).

#### Task 3a: Demais Projetos — grid 2x2 → blocos full-width (linhas 159-194)

- [x] **Passo 1: Substituir a tabela 2x2 por 4 blocos `<p align="center">`** – Concluído em 31/07/2026:08:29

  De: `<table>` com `<td width="50%">` (linhas 161-194).
  Para:

  ```markdown
  ### 📂 Demais Projetos

  <p align="center">
    <a href="https://github.com/tiagoeduardobr/Desafio_SCTEC">
      <img src="https://github-readme-stats-tiagoeduardobr.vercel.app/api/pin/?username=tiagoeduardobr&repo=Desafio_SCTEC&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="Desafio SCTEC"/>
    </a>
    <br/>
    <sub>Landing page BytePets — HTML, CSS, JS. Glassmorphism, acessível e responsivo.</sub>
  </p>

  <p align="center">
    <a href="https://github.com/tiagoeduardobr/Desafio_SCTEC_Analise_de_dados">
      <img src="https://github-readme-stats-tiagoeduardobr.vercel.app/api/pin/?username=tiagoeduardobr&repo=Desafio_SCTEC_Analise_de_dados&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="Análise de Dados"/>
    </a>
    <br/>
    <sub>Análise de dados com Python, Pandas e Jupyter Notebook.</sub>
  </p>

  <p align="center">
    <a href="https://github.com/tiagoeduardobr/opencode_termux">
      <img src="https://github-readme-stats-tiagoeduardobr.vercel.app/api/pin/?username=tiagoeduardobr&repo=opencode_termux&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="Opencode Termux"/>
    </a>
    <br/>
    <sub>Configuração do Opencode para Termux.</sub>
  </p>

  <p align="center">
    <a href="https://github.com/tiagoeduardobr/react_native">
      <img src="https://github-readme-stats-tiagoeduardobr.vercel.app/api/pin/?username=tiagoeduardobr&repo=react_native&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="React Native"/>
    </a>
    <br/>
    <sub>Desenvolvimento mobile com React Native.</sub>
  </p>
  ```

  > **Nota:** Repos, descrições (`<sub>`) e URLs custom do Vercel preservados exatamente. Cada projeto tem seu próprio bloco full-width.

#### Task 3b: Projeto Principal — tabela single-column → `<div>` (linhas 135-157)

> **Decisão do planner:** necessária para cumprir o critério de aceitação nº 1 ("nenhuma `<table>` usada para layout"). Conteúdo integralmente preservado.

- [x] **Passo 2: Substituir a tabela do "Projeto Principal" por `<div align="center">`** – Concluído em 31/07/2026:08:29

  De: `<table>` com `<td width="100%">` (linhas 135-157).
  Para:

  ```markdown
  ### 🏆 Projeto Principal

  <div align="center">
    <h3>
      <a href="https://parecer-descritivo.onrender.com">🚀 Parecer Descritivo</a>
    </h3>
    <p>
      <b>App web FastAPI + IA Generativa</b> — Gera pareceres descritivos para professores
      da Educação Infantil usando inteligência artificial.
    </p>
    <p>
      <a href="https://parecer-descritivo.onrender.com">
        <img src="https://img.shields.io/badge/Acessar_Produção-3fb950?style=for-the-badge&logo=render&logoColor=white" alt="Produção"/>
      </a>
    </p>
    <p align="left">
      <b>Stack:</b> Python, FastAPI, JavaScript, HTML5, CSS3, PostgreSQL, Docker, IA Generativa<br/>
      <b>Segurança:</b> JWT, Argon2, OWASP Top 10<br/>
      <b>Status:</b> 🟢 Em produção (plano gratuito — pode levar ~30s no primeiro acesso)
    </p>
  </div>
  ```

- [x] **Passo 3: Manter badge "Ver todos os repositórios" e verificar ausência de tabelas** – Concluído em 31/07/2026:08:29

  O bloco `<p align="center">` com o badge "Ver todos os repositórios" (linhas 196-200) permanece inalterado.

  Run: `grep -n "<table>\|</table>" README.md`
  Expected: sem output (nenhuma tabela restante no README).

**Critério de aceitação:** 4 projetos um por linha com `width="100%"` e links funcionando; "Projeto Principal" sem `<table>`; descrições e URLs preservadas; nenhuma `<table>` no arquivo.

---

### Task 4: Remover badges de paleta (linhas 16-27)

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

Remover apenas os 8 badges visíveis de cores e o separador `---` órfão. **MANTER** o comentário HTML das linhas 1-14 (documenta a paleta no código-fonte).

- [x] **Passo 1: Remover bloco de badges de paleta e separador órfão** – Concluído em 31/07/2026:08:00

  De: linhas 16-27 (bloco `<p align="center">` com 8 `<img>` de `img.shields.io/badge/Fundo-0d1117`, `Card-161b22`, `Texto-e6edf3`, `Borda-30363d`, `Destaque-58a6ff`, `Sucesso-3fb950`, `Atenção-d29922`, `IA-bc8cff` + linha em branco + `---`).
  Para: **remover tudo isso**, mantendo apenas o comentário da paleta e uma linha em branco antes do comentário `<!-- ===== HERO / HEADER ===== -->`.

  Resultado esperado no topo do arquivo:

  ```markdown
  <!--
  🎨 Paleta de Cores — Dark Mode (Perfil GitHub)
  ================================================
  Token              | Hex       | Uso
  --bg-primary       | #0d1117   | Fundo principal (GitHub Dark)
  --bg-card          | #161b22   | Fundo de cards/seções
  --text-primary     | #e6edf3   | Texto principal
  --text-secondary   | #8b949e   | Texto secundário
  --accent-blue      | #58a6ff   | Links, destaques, badges
  --accent-green     | #3fb950   | Sucesso, online, stats positivos
  --accent-orange    | #d29922   | Atenção, badges de linguagens
  --accent-purple    | #bc8cff   | Dados/IA badges
  --border           | #30363d   | Bordas e separadores
  -->

  <!-- ===== HERO / HEADER ===== -->
  ```

  > **Decisão do planner:** o `---` da linha 27 é removido porque, sem os badges, ele ficaria órfão entre o comentário (invisível) e o HERO — renderizando uma linha horizontal solta no topo. Os `---` das linhas 55, 222 e 230 (separadores entre seções visíveis) **permanecem**.

- [x] **Passo 2: Verificar remoção dos badges e manutenção do comentário** – Concluído em 31/07/2026:08:00

  Run: `grep -n "img.shields.io/badge/Fundo\|img.shields.io/badge/Card\|img.shields.io/badge/Texto\|img.shields.io/badge/IA-" README.md`
  Expected: sem output (badges de paleta removidos).

  Run: `grep -n "Paleta de Cores" README.md`
  Expected: linha 2 presente (comentário mantido).

**Critério de aceitação:** 8 badges de paleta removidos; comentário HTML da paleta (linhas 1-14) intacto; sem `---` órfão no topo; demais separadores e seções intactos.

---

### Task 5: Verificação final, revisão e commit

**Arquivos:** `README.md` (verificação; nenhuma edição)
**Complexidade:** Baixa
**Dependências:** Tasks 1-4

- [ ] **Passo 1: Rodar verificações estruturais**

  ```bash
  # 1. Nenhuma tabela restante
  grep -n "<table>\|</table>" README.md          # esperado: sem output

  # 2. Nenhum height fixo restante
  grep -n "height=\"180em\"" README.md           # esperado: sem output

  # 3. Nenhum wrapper anuraghazra restante
  grep -n "anuraghazra" README.md                # esperado: sem output

  # 4. Nenhum badge de paleta restante
  grep -n "img.shields.io/badge/Fundo" README.md # esperado: sem output

  # 5. Comentário da paleta mantido
  grep -n "Paleta de Cores" README.md            # esperado: linha 2 presente

  # 6. URLs custom do Vercel preservadas (Sobre mim stats, Analytics stats, top-langs, 4 pins)
  grep -c "github-readme-stats-tiagoeduardobr.vercel.app" README.md  # esperado: 7

  # 7. Cards com width="100%" (Sobre mim, stats, top-langs, streak, trophies, graph, 4 pins)
  grep -c 'width="100%"' README.md               # esperado: 10

  # 8. Linha do workflow intacta (sed do GitHub Actions)
  grep -n "Última atualização dos stats:" README.md  # esperado: linha presente com "</sub>"
  ```

- [ ] **Passo 2: Revisar visualmente no GitHub**

  - [ ] Preview desktop: todas as seções renderizam (Hero, Sobre mim, Tech Stack, GitHub Analytics, Projetos, Objetivo, Contato, rodapé)
  - [ ] Preview mobile (janela estreita / devtools): tudo empilha em coluna única; nenhum card cortado; nenhuma barra de rolagem horizontal
  - [ ] Cards de stats carregam (stats, top langs, streak, trophies, activity graph)
  - [ ] Links funcionam: parecer-descritivo.onrender.com, 4 repos de projetos, GitHub, LinkedIn, email
  - [ ] Paleta dark mode consistente em todo o documento
  - [ ] Nenhuma `<table>` visível

- [ ] **Passo 3: Revisão de código e commit (delegação)**

  - [ ] Rodar subagent `code-review` no diff (`git diff`) e corrigir problemas apontados
  - [ ] Delegar branch creation + commit para o subagent `git-commit` (ex.: branch `fix/responsividade-readme-mobile`)
  - [ ] Mensagem de commit no estilo do repositório: `fix: corrigir responsividade mobile do README do perfil`

**Critério de aceitação:** Todas as verificações estruturais passam (grep sem falhas), preview mobile sem quebras, code-review sem problemas bloqueadores, commit criado via `git-commit`.

---

## Cronograma de Implementação

| Task | Descrição | Dependência | Estimativa |
|------|-----------|------------|------------|
| 1 | Sobre mim: bullets + stats full-width | — | 10 min |
| 2 | GitHub Analytics: cards empilhados | — | 10 min |
| 3 | Projetos em Destaque: full-width (3a grid + 3b destaque) | — | 20 min |
| 4 | Remover badges de paleta + separador órfão | — | 10 min |
| 5 | Verificação final, revisão e commit | Tasks 1-4 | 20 min |

**Total estimado:** ~1 hora

> **Nota de ordem de aplicação:** Tasks 1-4 são independentes, mas editam o mesmo arquivo. Para diffs limpos, aplicar de cima para baixo no arquivo: **Task 4 → Task 1 → Task 2 → Task 3** (ou identificar cada seção pelo heading/conteúdo, não por line number — as linhas mudam a cada edição).

---

## Riscos e Mitigações

| Risco | Mitigação |
|-------|-----------|
| Reverter URLs custom do Vercel para o host genérico (commit `815af18`) | Verificação estrutural nº 6 (grep conta 7 ocorrências do host custom); usar markup exato do plano |
| Quebrar a linha "Última atualização dos stats:" que o workflow `update-stats.yml` edita via `sed` | Não tocar seções de rodapé (Task 5 verifica a linha intacta) |
| `<sub>` dentro de `<p>` renderizar com espaçamento estranho | Padrão já usado no README atual (linhas 168, 175, 184, 191); manter conforme spec |
| Tabela remanescente não detectada (ex.: `</table>` sem `<table>`) | Grep cobre `<table>` e `</table>`; revisão visual confirma |
| Serviço de stats fora do ar | README continua funcional sem os cards; links e textos permanecem |
| Badge de produção com `&` na URL quebrando parse do markdown | Mesmo markup já renderiza hoje (linha 147); GitHub tolera `&` cru em URLs de imagem |
| Grid 2x2 removido mas conteúdo duplicado/perdido | Revisão visual confirma exatamente 4 projetos + 1 destaque; grep conta pins (`/api/pin/` = 4 ocorrências) |

---

## Verificação Final

Antes de marcar como concluído:

- [ ] Nenhuma `<table>` ou `</table>` no README.md
- [ ] Nenhum `height="180em"` restante
- [ ] Nenhum wrapper `<a href="https://github.com/anuraghazra/github-readme-stats">`
- [ ] Todos os cards de stats com `width="100%"` (10 ocorrências)
- [ ] 4 projetos em destaque um por linha, com descrições preservadas
- [ ] 8 badges de paleta removidos; comentário HTML da paleta mantido (linha 2 `Paleta de Cores`)
- [ ] Separador `---` órfão do topo removido; demais separadores preservados
- [ ] URLs custom do Vercel preservadas (7 ocorrências de `github-readme-stats-tiagoeduardobr.vercel.app`)
- [ ] Linha "Última atualização dos stats:" intacta (compatibilidade com GitHub Actions)
- [ ] Paleta dark mode e seções Hero, Tech Stack, Objetivo, Contato e rodapé intactas
- [ ] Links funcionando (parecer-descritivo.onrender.com, repos, LinkedIn, email)
- [ ] Preview mobile no GitHub sem quebras (coluna única, sem scroll horizontal)
- [ ] Code-review concluído sem problemas bloqueadores
- [ ] Commit criado via `git-commit` (branch `fix/responsividade-readme-mobile`)

---

## Alterações em relação ao plano v2

| Item | v2 (atual) | v3 (este plano) |
|------|-----------|-----------------|
| "Sobre mim" | Tabela 60%/40% (texto + stats lado a lado) | Bullets markdown + stats card `width="100%"` abaixo |
| GitHub Analytics | Stats + Top Langs `height="180em"` dentro de `<a>` | Cards empilhados `width="100%"`, sem wrapper `<a>`, sem height fixo |
| Demais Projetos | Grid 2x2 com `<td width="50%">` | 4 blocos full-width um por linha |
| Projeto Principal | Tabela single-column `<td width="100%">` | `<div align="center">` (cumpre critério "sem tabela") |
| Badges de paleta | 8 badges visíveis no topo | Removidos; comentário HTML da paleta mantido |
| Separador do topo | `---` após badges | Removido (órfão) |
| Responsividade mobile | Tabelas (quebram no mobile) | Full-width empilhado (100% confiável no GitHub) |

---

*Plano criado em 30/07/2026 às 22:45 UTC pelo Task Planner Agent — baseado na spec aprovada de correção de responsividade e no formato do plano v2 (20260729_0737).*
