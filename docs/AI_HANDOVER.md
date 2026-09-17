# AI Handover — Perfil GitHub Tiago Eduardo Zimmermann

> Última atualização: 2026-09-17

## 1. Projeto

Criar e manter um **perfil GitHub profissional** para Tiago Eduardo Zimmermann (Desenvolvedor de Software | Python | Full-Stack | React | APIs REST | IA Generativa). O README.md do perfil inclui:

- **H1**: "Olá, eu sou Tiago Eduardo Zimmermann 👋" + título "Desenvolvedor de Software | Python | Full-Stack | React | APIs REST | IA Generativa" + 4 badges (LinkedIn, GitHub, E-mail, Parecer Descritivo)
- **Sobre mim**: 3 parágrafos — transição de carreira (~25 anos automotiva + TC Mecânica), competências transferíveis, formação ADS
- **Atualmente**: 5 bullets (ADS UNIASSELVI, React Native SCTEC, migração gradual React, agentes IA/SDD, Linux/Termux)
- **Projeto em destaque: Parecer Descritivo**: tabela de tecnologias (FastAPI, PostgreSQL/Neon, JS/HTML/CSS → React gradual, Docker/Git/CI/CD/Render, Groq+GPT-OSS-20B, JWT), 201 testes, LGPD práticas, AI-Assisted
- **Stack e tecnologias**: "Em uso" (16 badges) + "Em estudo / experimentação" (7 badges)
- **Inteligência Artificial**: 4 bullets (IA Generativa/LLMs, modelos open source, orquestração de agentes, AI-Assisted com supervisão humana)
- **Engenharia de Software**: 7 bullets (APIs REST, testes 201, CI/CD, Docker, PostgreSQL, SDD em estudo, Git/GitHub)
- **Formação**: tabela 3 cursos (ADS UNIASSELVI fev/2025-jun/2027 em andamento, Entra21/SENAI-SC jan/2025-set/2025 concluído, React Native SCTEC em andamento)
- **Outros projetos**: tabela 7 projetos (BytePets, Análise de Dados, Curso_Pessoal_Python, prompt-mentor, desafioIA_react_native, opencode_termux, react_native)
- **Conecte-se comigo**: 4 badges
- **Stats**: 2 cards empilhados (stats deploy próprio + streak herokuapp)
- **Footer**: badge "Feito com ❤", linha "Última atualização dos stats: 17/09/2026 às 19:35 UTC" (formato sed preservado), copyright

**Ordem atual das seções**: H1 → Sobre mim → Atualmente → Projeto em destaque → Stack e tecnologias → Inteligência Artificial → Engenharia de Software → Formação → Outros projetos → Conecte-se comigo → Stats → Footer

## 2. Serviços Vercel (Self-hosted)

O GitHub bloqueou os serviços públicos (503 DEPLOYMENT_PAUSED / 402 DEPLOYMENT_DISABLED). Criamos deploys próprios no Vercel:

| Serviço | URL | Fork de | Status |
|---|---|---|---|
| **Stats/Top Langs/Pins** | `github-readme-stats-tiagoeduardobr.vercel.app` | anuraghazra/github-readme-stats | ✅ Funcionando (PAT_1 renovado 17/09/2026) |
| **Trophies** | `github-profile-trophy-erunocarm-tiagoeduardobrs-projects.vercel.app` | ryo-ma/github-profile-trophy | ❌ FUNCTION_INVOCATION_FAILED (GITHUB_TOKEN1/2 não configurados) |
| **Activity Graph** | `github-readme-activity-graph.vercel.app` (público) | ashutosh00710/github-readme-activity-graph | ❌ DEPLOYMENT_DISABLED (HTTP 402) |

> **Nota**: Trophies e Activity Graph foram **removidos integralmente** na reescrita do README (f4a28ea) — não há HTML comments. Reativação exige re-adicionar os blocos ao README (referência: plano `20260917_0710_refatorar-readme-perfil.md`, Task 5) e solução própria (instância própria ou tokens configurados).

## 3. Variáveis de Ambiente Necessárias

### Para Stats (github-readme-stats):
- **`PAT_1`**: Token GitHub pessoal (Fine-grained ou Classic) — ✅ **renovado e funcionando** (17/09/2026)

### Para Trophies (github-profile-trophy):
- **`GITHUB_TOKEN1`**: Token GitHub pessoal — **ainda NÃO configurado**
- **`GITHUB_TOKEN2`**: Mesmo token (fallback) — **ainda NÃO configurado**
- Runtime: **Deno** (`vercel-deno@3.1.1`) — o Vercel precisa detectar automaticamente
- Deploy Protection: deve estar em **"Only for Preview Deployments"** (SSO causa 302 → vercel.com/login)
- **Ainda retorna HTTP 500 FUNCTION_INVOCATION_FAILED** — precisa adicionar as env vars e redeploy

### Como criar o token GitHub:
1. github.com > Settings > Developer settings > Personal access tokens > Fine-grained tokens
2. Generate new token
3. Repository access: "Only select repositories" → `tiagoeduardobr`
4. Permissions: sem permissões especiais necessárias (dados são públicos)
5. Expiration: 90 dias (renovar depois)

<!-- Verificar requisitos de permissão ao reativar Trophies — pode precisar de scope adicional -->

## 4. GitHub Actions Workflow

**Arquivo**: `.github/workflows/update-stats.yml`

- Cron: `0 6 * * *` (6h UTC diariamente)
- Permissões: `contents: write`
- Comando: `sed -i` para atualizar a linha "Última atualização dos stats: DATA</sub>" no README.md
- Commit com `[skip ci]` para evitar loop
- **Requer token com scope `workflow`** (o user já corrigiu isso)

## 5. Regras e Convenções Aprendidas

### 🚨 REGRAS CRÍTICAS:
1. **NUNCA rodar comandos git de escrita diretamente** — sempre delegar para o agente `git-commit`. Isso inclui: `git push`, `git commit`, `git merge`, `git checkout -b`, `git branch -d`
2. **Leitura git permitida diretamente**: `git status`, `git log`, `git diff`
3. **O modelo não suporta imagens** — verificação é via curl/webfetch, nunca por screenshot
4. **Testar antes de aplicar** — o usuário prefere que testemos endpoints (curl HTTP 200) antes de aplicar mudanças no README

### Decisões de design:
- **Layout 100% full-width** — GitHub strips media queries do README, então tudo precisa empilhar sem `<table>`
- **Sem badges de paleta** — confundiam visitantes (removidos integralmente na reescrita f4a28ea)
- **Cards empilhados** — Analytics e Projetos ficam melhor um por linha no mobile
- **Trophies/Graph removidos integralmente na reescrita** (17/09/2026) — sem HTML comments; reativar quando serviços responderem HTTP 200, re-adicionando os blocos ao README

## 6. Commits Importantes

| Hash | Descrição |
|---|---|
| `2b67b11` | feat: reescrever perfil GitHub (10 tasks do plano v2) |
| `815af18` | fix: trocar URLs do github-readme-stats para deploy próprio no Vercel |
| `42f4a07` | fix: corrigir responsividade mobile do README do perfil |
| `5fd43d2` | Merge para main |
| `04155b7` | refactor: reestruturar README do perfil GitHub (hero unificado, stack enxuta, seções reordenadas) |
| `f48d3b2` | Merge branch 'feature/refatorar-readme-perfil' para main |
| `f4a28ea` | docs: reescrever README com perfil profissional (reescrita integral, 163 linhas) |

## 7. Status Atual

- ✅ README reescrito integralmente (163 linhas, 9 seções, 32 badges — 17/09/2026)
- ✅ Stats/Top Langs/Pins funcionando via Vercel próprio (PAT_1 renovado)
- ✅ GitHub Actions atualizando stats diariamente
- ❌ Trophies: removido do README (não comentado) — precisa configurar `GITHUB_TOKEN1` e `GITHUB_TOKEN2` no Vercel e re-adicionar o bloco ao README
- ❌ Activity Graph: removido do README (não comentado) — instância pública retorna 402 (DEPLOYMENT_DISABLED), precisa instância própria e re-adicionar o bloco
- 📝 Planos em `.opencode/plans/`: v2 (10 tasks, concluído), responsividade (Tasks 1-4 concluídas, Task 5 de verificação/commit pendente), refatorar-readme-perfil (concluído)

## 8. Estrutura do Projeto

```
/root/Projetos/tiagoeduardobr/
├── README.md                    # Perfil GitHub (~163 linhas, reescrito 17/09/2026)
├── .github/
│   └── workflows/
│       └── update-stats.yml     # Cron diário para atualizar stats
├── docs/
│   └── AI_HANDOVER.md           # Este arquivo
└── .opencode/
    └── plans/
        ├── 20260728_2125_melhorar-perfil-github.md
        ├── 20260729_0737_melhorar-perfil-github-v2.md
        ├── 20260730_2245_corrigir-responsividade-readme.md
        └── 20260917_0710_refatorar-readme-perfil.md      # ✅ Concluído (plano concluído para o estado `04155b7`, superado pela reescrita integral `f4a28ea`)
```

## 9. Próximos Passos

1. **Configurar `GITHUB_TOKEN1` e `GITHUB_TOKEN2`** no Vercel (projeto github-profile-trophy) + redeploy
2. **Testar URL do trophy** com curl (HTTP 200 + SVG)
3. **Reativar Trophies no README** — re-adicionar bloco (referência: plano `20260917_0710_refatorar-readme-perfil.md`, Task 5), trocar para URL própria
4. **Avaliar deploy próprio do Activity Graph** — instância pública retorna 402, precisa solução própria
5. **Reativar Activity Graph no README** quando instância própria funcionar
6. **Commit via `git-commit` agent**

---

**Importante**: Este handover deve ser atualizado sempre que houver mudanças significativas no projeto.
