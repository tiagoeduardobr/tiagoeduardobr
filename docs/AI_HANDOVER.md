# AI Handover — Perfil GitHub Tiago Eduardo Zimmermann

> Última atualização: 2026-09-17

## 1. Projeto

Criar e manter um **perfil GitHub profissional** para Tiago Eduardo Zimmermann (Desenvolvedor Júnior em Blumenau/SC). O README.md do perfil inclui:

- **Hero**: Typing SVG "Eu sou" + "Tiago Eduardo Zimmermann" (split em 2 linhas) + badges (Localização, Disponibilidade, Nível) + contadores (Visitantes, Seguidores) + parágrafo descritivo — única introdução (H1 duplicado removido na refatoração de 17/09/2026)
- **Sobre mim**: 6 bullets + card de stats GitHub (`width="100%"`)
- **Projetos em Destaque**: 4 projetos um por linha (`<p align="center">`) + badge "Ver todos repos"
- **Tech Stack**: 10 badges simplificados (TypeScript, React, React Native, Python, FastAPI, SQL, Pandas, Jupyter Notebook, Git, Docker) — de 17 para 10 na refatoração
- **GitHub Analytics**: Stats + Top Langs + Streak empilhados full-width (cards duplicados removidos)
- **Contato**: links de contato
- **Footer**: "Última atualização dos stats" + badge "Feito com ❤ por Tiago Eduardo Zimmermann" + copyright

**Seções removidas na refatoração (17/09/2026):**
- H1 duplicado "Olá, eu sou o Tiago Eduardo Zimmermann!" (hero com typing SVG é a única introdução)
- Stats duplicado (card agora só na seção Analytics)
- Seção "🎯 Objetivo" (repetia hero e Sobre mim)
- Trophies e Activity Graph (temporariamente — comentados com HTML comment documentando reativação)

**Ordem atual das seções**: Hero → Sobre mim → Projetos em Destaque → Tech Stack → GitHub Analytics → Contato → Footer

## 2. Serviços Vercel (Self-hosted)

O GitHub bloqueou os serviços públicos (503 DEPLOYMENT_PAUSED / 402 DEPLOYMENT_DISABLED). Criamos deploys próprios no Vercel:

| Serviço | URL | Fork de | Status |
|---|---|---|---|
| **Stats/Top Langs/Pins** | `github-readme-stats-tiagoeduardobr.vercel.app` | anuraghazra/github-readme-stats | ✅ Funcionando (PAT_1 renovado 17/09/2026) |
| **Trophies** | `github-profile-trophy-erunocarm-tiagoeduardobrs-projects.vercel.app` | ryo-ma/github-profile-trophy | ❌ FUNCTION_INVOCATION_FAILED (GITHUB_TOKEN1/2 não configurados) |
| **Activity Graph** | `github-readme-activity-graph.vercel.app` (público) | ashutosh00710/github-readme-activity-graph | ❌ DEPLOYMENT_DISABLED (HTTP 402) |

> **Nota**: Trophies e Activity Graph estão **comentados no README** com HTML comments documentando reativação. Ambos precisam de solução própria (instância própria ou tokens configurados) antes de serem reativados.

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
- **Sem badges de paleta** — confundiam visitantes (mantidos apenas como HTML comment)
- **Cards empilhados** — Analytics e Projetos ficam melhor um por linha no mobile
- **Typing SVG split** — "Eu+sou" e "Tiago+Eduardo+Zimmermann" em linhas separadas para não cortar
- **Trophies/Graph removidos temporariamente** (17/09/2026) — substituídos por HTML comments documentando reativação; reativar quando serviços responderem HTTP 200

## 6. Commits Importantes

| Hash | Descrição |
|---|---|
| `2b67b11` | feat: reescrever perfil GitHub (10 tasks do plano v2) |
| `815af18` | fix: trocar URLs do github-readme-stats para deploy próprio no Vercel |
| `42f4a07` | fix: corrigir responsividade mobile do README do perfil |
| `5fd43d2` | Merge para main |
| `04155b7` | refactor: reestruturar README do perfil GitHub (hero unificado, stack enxuta, seções reordenadas) |
| `f48d3b2` | Merge branch 'feature/refatorar-readme-perfil' para main |

## 7. Status Atual

- ✅ README refatorado (hero unificado, 10 badges stack, seções reordenadas — 17/09/2026)
- ✅ Stats/Top Langs/Pins funcionando via Vercel próprio (PAT_1 renovado)
- ✅ GitHub Actions atualizando stats diariamente
- ✅ Paleta de cores documentada (HTML comment)
- ❌ Trophies: comentado no README — precisa configurar `GITHUB_TOKEN1` e `GITHUB_TOKEN2` no Vercel e reativar
- ❌ Activity Graph: comentado no README — instância pública retorna 402 (DEPLOYMENT_DISABLED), precisa instância própria
- 📝 Planos em `.opencode/plans/`: v2 (10 tasks, concluído), responsividade (Tasks 1-4 concluídas, Task 5 pendente até trophy funcionar), refatorar-readme-perfil (concluído)

## 8. Estrutura do Projeto

```
/root/Projetos/tiagoeduardobr/
├── README.md                    # Perfil GitHub (~210 linhas, refatorado 17/09/2026)
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
        └── 20260917_0710_refatorar-readme-perfil.md      # ✅ Concluído
```

## 9. Próximos Passos

1. **Configurar `GITHUB_TOKEN1` e `GITHUB_TOKEN2`** no Vercel (projeto github-profile-trophy) + redeploy
2. **Testar URL do trophy** com curl (HTTP 200 + SVG)
3. **Reativar Trophies no README** — descomentar HTML comment, trocar para URL própria
4. **Avaliar deploy próprio do Activity Graph** — instância pública retorna 402, precisa solução própria
5. **Reativar Activity Graph no README** quando instância própria funcionar
6. **Commit via `git-commit` agent**

---

**Importante**: Este handover deve ser atualizado sempre que houver mudanças significativas no projeto.
