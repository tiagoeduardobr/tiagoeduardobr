# AI Handover — Perfil GitHub Tiago Eduardo Zimmermann

> Última atualização: 2026-07-31

## 1. Projeto

Criar e manter um **perfil GitHub profissional** para Tiago Eduardo Zimmermann (Desenvolvedor Júnior em Blumenau/SC). O README.md do perfil inclui:

- **H1**: `# Olá, eu sou o Tiago Eduardo Zimmermann 👯`
- **Typing SVG**: "Eu sou" + "Tiago Eduardo Zimmermann" (split em 2 linhas para não cortar)
- **Descrição**: "Desenvolvedor Júnior em Blumenau/SC, buscando transformar ideias em soluções digitais práticas e de impacto."
- **Sobre mim**: 6 bullets + card de stats GitHub (`width="100%"`)
- **GitHub Analytics**: 5 cards empilhados full-width (Stats, Top Langs, Streak, Trophies, GitHub Graph)
- **Projetos**: 4 projetos um por linha (`<p align="center">`) + badge "Ver todos repos"
- **Footer**: "Última atualização dos stats" + badge "Feito com ❤ por Tiago Eduardo Zimmermann" + copyright

## 2. Serviços Vercel (Self-hosted)

O GitHub bloqueou os serviços públicos (503 DEPLOYMENT_PAUSED / 402 DEPLOYMENT_DISABLED). Criamos deploys próprios no Vercel:

| Serviço | URL | Fork de | Status |
|---|---|---|---|
| **Stats/Top Langs/Pins** | `github-readme-stats-tiagoeduardobr.vercel.app` | anuraghazra/github-readme-stats | ✅ Funcionando |
| **Trophies** | `github-profile-trophy-erunocarm-tiagoeduardobrs-projects.vercel.app` | ryo-ma/github-profile-trophy | ❌ FUNCTION_INVOCATION_FAILED |

## 3. Variáveis de Ambiente Necessárias

### Para Stats (github-readme-stats):
- **`PAT_1`**: Token GitHub pessoal (Fine-grained ou Classic) — já configurado e funcionando

### Para Trophies (github-profile-trophy):
- **`GITHUB_TOKEN1`**: Token GitHub pessoal — **NÃO CONFIGURADO AINDA**
- **`GITHUB_TOKEN2`**: Mesmo token (fallback) — **NÃO CONFIGURADO AINDA**
- Runtime: **Deno** (`vercel-deno@3.1.1`) — o Vercel precisa detectar automaticamente
- Deploy Protection: deve estar em **"Only for Preview Deployments"** (SSO causa 302 → vercel.com/login)
- **Ainda retorna HTTP 500 FUNCTION_INVOCATION_FAILED** — precisa adicionar as env vars e redeploy

### Como criar o token GitHub:
1. github.com > Settings > Developer settings > Personal access tokens > Fine-grained tokens
2. Generate new token
3. Repository access: "Only select repositories" → `tiagoeduardobr`
4. Permissions: sem permissões especiais necessárias (dados são públicos)
5. Expiration: 90 dias (renovar depois)

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

## 6. Commits Importantes

| Hash | Descrição |
|---|---|
| `2b67b11` | feat: reescrever perfil GitHub (10 tasks do plano v2) |
| `815af18` | fix: trocar URLs do github-readme-stats para deploy próprio no Vercel |
| `42f4a07` | fix: corrigir responsividade mobile do README do perfil |
| `5fd43d2` | Merge para main |

## 7. Status Atual

- ✅ README profissional completo (dark mode, responsivo, full-width)
- ✅ Stats/Top Langs/Pins funcionando via Vercel próprio
- ✅ GitHub Actions atualizando stats diariamente
- ✅ Paleta de cores documentada (HTML comment)
- ❌ Trophies: precisa configurar `GITHUB_TOKEN1` e `GITHUB_TOKEN2` no Vercel
- 📝 Planos em `.opencode/plans/`: v2 (10 tasks, concluído) e responsividade (Tasks 1-4 concluídas, Task 5 pendente até trophy funcionar)

## 8. Estrutura do Projeto

```
/root/Projetos/tiagoeduardobr/
├── README.md                    # Perfil GitHub (210 linhas)
├── .github/
│   └── workflows/
│       └── update-stats.yml     # Cron diário para atualizar stats
├── docs/
│   └── AI_HANDOVER.md           # Este arquivo
└── .opencode/
    └── plans/
        ├── 20260729_0737_melhorar-perfil-github-v2.md
        └── 20260730_2245_corrigir-responsividade-readme.md
```

## 9. Próximos Passos

1. **URGENTE**: Usuário deve adicionar `GITHUB_TOKEN1` e `GITHUB_TOKEN2` no Vercel (projeto github-profile-trophy) e redeploy
2. Testar URL do trophy com curl (HTTP 200 + SVG)
3. Atualizar URL do trophy no README.md (trocar `github-profile-trophy.vercel.app` pela URL própria)
4. Commit via `git-commit` agent
5. Marcar Task 5 (verificação final) como concluída no plano de responsividade

---

**Importante**: Este handover deve ser atualizado sempre que houver mudanças significativas no projeto.
