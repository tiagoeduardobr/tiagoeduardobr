# Plano: Melhoria do Perfil GitHub — tiagoeduardobr

> **Para workers agentic:** Usar `subagent-driven-development` (recomendado) ou `executing-plans` para implementar este plano tarefa por tarefa.
> Passos usam checkbox (`- [ ]`) para tracking.

**Objetivo:** Transformar o README do perfil GitHub de tiagoeduardobr em uma vitrine profissional moderna com design dark mode, stats dinâmicos, seção de portfólio e automação via GitHub Actions.

**Arquitetura:** README.md único (repositório especial de perfil) com markdown enriquecido + GitHub Actions para atualização diária de stats. Uso de serviços externos (github-readme-stats, github-profile-trophy, streak-stats) para cards dinâmicos. Design 100% responsivo via markdown + SVG.

**Tech Stack:** Markdown, HTML (inline no README), GitHub Actions (YAML), Shields.io (badges), GitHub Readme Stats (cards), GitHub Profile Trophy, GitHub Streak Stats.

**Stack detectada:** Repositório de perfil GitHub (README.md). Nenhuma stack de desenvolvimento de aplicação detectada. Skills carregadas: `spec-driven-development`, `executing-plans`, `frontend-complete`, `devops-engineer`, `writing-plans`.

---

## Premissas / Assumptions

1. O repositório `tiagoeduardobr/tiagoeduardobr` é o repositório especial de perfil do GitHub — apenas `README.md` e `.github/workflows/` serão modificados.
2. O perfil deve ser dark mode profissional com identidade visual consistente.
3. Os stats cards serão servidos por serviços gratuitos (github-readme-stats.vercel.app, github-readme-streak-stats.herokuapp.com, github-profile-trophy.vercel.app).
4. Os projetos em destaque virão dos pinned repositories do perfil GitHub do usuário.
5. A automação via GitHub Actions rodará diariamente (cron schedule).
6. O tom do texto será profissional e direto.

---

## Escopo

### Dentro
- Redesign completo do README.md com identidade visual dark mode
- Header/Hero com apresentação profissional
- Seção "Sobre mim" refinada com ícones e estrutura melhorada
- Seção "Tech Stack" com badges organizados por categoria e com cores temáticas
- Seção "GitHub Stats" com cards dinâmicos (stats, top langs, streak, trophies)
- Seção "Portfólio / Projetos em Destaque" com os pinned repos
- Seção "Contato" com badges sociais
- GitHub Actions workflow para atualização diária de stats
- Rodapé com contador de visitas e ano atual

### Fora
- Não serão criados novos repositórios
- Não serão modificados pinned repositories no GitHub (apenas referenciados)
- Não será usado JavaScript no README (apenas markdown + HTML estático)
- Não serão criados sites externos ou landing pages
- Não serão incluídos analytics ou tracking

---

## Tasks

### Task 1: Definir identidade visual e paleta de cores

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

Definir o sistema de design do perfil antes de começar a escrever conteúdo. Estabelecer paleta, tom e regras visuais.

- [ ] **Passo 1: Definir paleta de cores dark mode**

  Paleta definida para o perfil:

  | Token | Hex | Uso |
  |-------|-----|-----|
  | `--bg-primary` | `#0d1117` | Fundo principal (GitHub Dark) |
  | `--bg-card` | `#161b22` | Fundo de cards/seções |
  | `--text-primary` | `#e6edf3` | Texto principal |
  | `--text-secondary` | `#8b949e` | Texto secundário |
  | `--accent-blue` | `#58a6ff` | Links, destaques, badges |
  | `--accent-green` | `#3fb950` | Sucesso, online, stats positivos |
  | `--accent-orange` | `#d29922` | Atenção, badges de linguagens |
  | `--accent-purple` | `#bc8cff` | Dados/IA badges |
  | `--border` | `#30363d` | Bordas e separadores |

- [ ] **Passo 2: Definir identidade visual**

  - Background: `#0d1117` (mesmo fundo do GitHub Dark)
  - Heading style: Uso de badges/ícones como separadores visuais (ex: `### 🚀 Sobre mim` já existente)
  - Cards: Caixas delimitadas com `<!--- ... --->` ou tabelas com bordas para simular cards
  - Badges: Shields.io com logo colorido e fundo escuro (`style=for-the-badge`)
  - Divisores visuais: Linhas horizontais com `---` ou separadores temáticos
  - Fonte: Monospace para código, sans-serif para texto corrido (padrão GitHub)
  - Responsividade: Tabelas com `width=100%` e imagens com `max-width=100%`

**Critério de aceitação:** Paleta documentada e consistente. Identidade visual definida e aprovada.

---

### Task 2: Criar seção Hero / Header

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1

Criar um header impactante com apresentação, cargo, localização e badges de saudação.

- [ ] **Passo 1: Escrever header com apresentação profissional**

  ```markdown
  <div align="center">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=28&duration=3000&pause=500&color=58A6FF&center=true&vCenter=true&width=435&lines=Olá,+eu+sou+Tiago+Eduardo;Full-Stack+Developer;E-commerce+Architect;Python+%26+AI+Enthusiast" alt="Typing SVG" />
    
    <p align="center">
      <img src="https://img.shields.io/badge/Blumenau-SC-58a6ff?style=flat-square&logo=google-maps&logoColor=white" alt="Location"/>
      <img src="https://img.shields.io/badge/Disponível%20para-REMOTO-3fb950?style=flat-square&logo=remote&logoColor=white" alt="Availability"/>
      <img src="https://img.shields.io/badge/Foco-E--commerce-d29922?style=flat-square&logo=shopify&logoColor=white" alt="Focus"/>
    </p>
  </div>
  ```

- [ ] **Passo 2: Adicionar badge de visitas e saudação**

  ```markdown
  <p align="center">
    <img src="https://komarev.com/ghpvc/?username=tiagoeduardobr&color=58a6ff&style=flat-square&label=Visitantes" alt="Profile views"/>
    <img src="https://img.shields.io/github/followers/tiagoeduardobr?label=Seguidores&style=flat-square&color=3fb950" alt="Followers"/>
  </p>
  ```

- [ ] **Passo 3: Adicionar breve descrição profissional**

  ```markdown
  <p align="center">
    <b>Desenvolvedor Full-Stack</b> em Blumenau/SC, focado em arquitetura de plataformas de e-commerce, 
    otimização de performance e integração de IA. Transformo ideias complexas em soluções digitais escaláveis.
  </p>
  ```

**Critério de aceitação:** Header com typing effect, badges de localização/disponibilidade, contador de visitas e descrição profissional. Tudo alinhado e responsivo.

---

### Task 3: Refatorar seção "Sobre Mim"

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1

Reestruturar a seção "Sobre mim" com ícones temáticos e texto profissional direto.

- [ ] **Passo 1: Reescrever a seção Sobre Mim com ícones e estrutura melhorada**

  ```markdown
  ## 🚀 Sobre mim

  <table>
    <tr>
      <td width="60%">
        
  - 🛒 **E-commerce Architect** — Arquitetura de plataformas de e-commerce ponta a ponta com APIs otimizadas e automações
  - ⚡ **Performance-Driven** — Melhorias de performance com foco em redução de carregamento e UX
  - ♿ **Acessibilidade First** — Priorizo WCAG, SEO técnico e boas práticas de experiência do usuário
  - 🎓 **Formação** — Cursando Análise e Desenvolvimento de Sistemas, com aprendizado contínuo em Software, Dados e IA
  - 🤝 **Colaborações** — Aberto a parcerias com startups inovadoras e projetos de impacto
        
      </td>
      <td width="40%" align="center">
        <img src="https://github-readme-stats.vercel.app/api?username=tiagoeduardobr&show_icons=true&theme=github_dark&hide_border=true&count_private=true&bg_color=0d1117&icon_color=58a6ff&text_color=c9d1d9&title_color=58a6ff" width="100%" alt="GitHub Stats"/>
      </td>
    </tr>
  </table>
  ```

- [ ] **Passo 2: Verificar alinhamento e responsividade**

  Testar visualmente que a tabela funciona em mobile (as colunas empilham corretamente). O GitHub Markdown renderiza tabelas naturalmente responsivas.

**Critério de aceitação:** Seção "Sobre mim" com ícones, bullets claros, e mini stats card lateral. Tom profissional e direto.

---

### Task 4: Criar seção "Tech Stack" com badges organizados por categoria

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Task 1

Organizar as tecnologias em categorias visuais com badges modernos (style=for-the-badge) e cores por categoria.

- [ ] **Passo 1: Adicionar seção Frontend**

  ```markdown
  ## 🛠️ Tech Stack

  ### 🎨 Frontend
  ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
  ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
  ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
  ![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
  ```

- [ ] **Passo 2: Adicionar seção Backend**

  ```markdown
  ### 🐍 Backend
  ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
  ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
  ![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
  ![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white)
  ```

- [ ] **Passo 3: Adicionar seção Data & AI**

  ```markdown
  ### 📊 Data & AI
  ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
  ![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
  ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
  ```

- [ ] **Passo 4: Adicionar seção Tools & DevOps**

  ```markdown
  ### 🛠️ Tools & DevOps
  ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
  ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
  ![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
  ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
  ```

**Critério de aceitação:** 4 categorias de tecnologias com badges coloridos e consistentes. Layout limpo e responsivo. Badges no formato `for-the-badge` com logos coloridos.

---

### Task 5: Criar seção de GitHub Stats com cards dinâmicos

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Task 1

Adicionar cards de estatísticas do GitHub usando a API github-readme-stats e serviços complementares.

- [ ] **Passo 1: Adicionar linha de stats cards (2 colunas)**

  ```markdown
  ## 📈 GitHub Analytics

  <div align="center">
    <a href="https://github.com/anuraghazra/github-readme-stats">
      <img height="180em" src="https://github-readme-stats.vercel.app/api?username=tiagoeduardobr&show_icons=true&theme=github_dark&hide_border=true&count_private=true&bg_color=0d1117&icon_color=58a6ff&text_color=c9d1d9&title_color=58a6ff" />
      <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=tiagoeduardobr&layout=compact&langs_count=6&theme=github_dark&hide_border=true&bg_color=0d1117&text_color=c9d1d9&title_color=58a6ff" />
    </a>
  </div>
  ```

- [ ] **Passo 2: Adicionar streak stats**

  ```markdown
  <div align="center">
    <img src="https://github-readme-streak-stats.herokuapp.com/?user=tiagoeduardobr&theme=github-dark-blue&hide_border=true&background=0d1117&stroke=58a6ff&ring=58a6ff&fire=3fb950&currStreakLabel=58a6ff" width="100%" alt="GitHub Streak"/>
  </div>
  ```

- [ ] **Passo 3: Adicionar trophy case**

  ```markdown
  <div align="center">
    <img src="https://github-profile-trophy.vercel.app/?username=tiagoeduardobr&theme=onestar&no-frame=true&no-bg=true&row=2&column=3&margin-w=15&margin-h=15" width="100%" alt="GitHub Trophies"/>
  </div>
  ```

- [ ] **Passo 4: Adicionar gráfico de contribuições**

  ```markdown
  <div align="center">
    <img src="https://github-readme-activity-graph.vercel.app/graph?username=tiagoeduardobr&theme=github-dark&bg_color=0d1117&hide_border=true&point=58a6ff&color=58a6ff&line=3fb950&area=true" width="100%" alt="Contribution Graph"/>
  </div>
  ```

**Critério de aceitação:** 4 cards dinâmicos visíveis: stats, top langs, streak, trophies. Tema escuro consistente. Links funcionando. Dados reais do GitHub sendo exibidos.

---

### Task 6: Criar seção de Portfólio / Projetos em Destaque

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Task 1

Exibir os principais projetos do usuário (pinned repos) com descrições e links.

- [ ] **Passo 1: Adicionar seção de projetos com cards em tabela**

  ```markdown
  ## 📌 Projetos em Destaque

  <table>
    <tr>
      <td width="50%" align="center">
        <a href="https://github.com/tiagoeduardobr/Desafio_SCTEC">
          <img src="https://github-readme-stats.vercel.app/api/pin/?username=tiagoeduardobr&repo=Desafio_SCTEC&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="Desafio SCTEC"/>
        </a>
        <br/>
        <sub>Landing page BytePets — HTML, CSS, JS. Glassmorphism, acessível e responsivo.</sub>
      </td>
      <td width="50%" align="center">
        <a href="https://github.com/tiagoeduardobr/Desafio_SCTEC_Analise_de_dados">
          <img src="https://github-readme-stats.vercel.app/api/pin/?username=tiagoeduardobr&repo=Desafio_SCTEC_Analise_de_dados&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="Análise de Dados"/>
        </a>
        <br/>
        <sub>Análise de dados com Python, Pandas e Jupyter Notebook.</sub>
      </td>
    </tr>
    <tr>
      <td width="50%" align="center">
        <a href="https://github.com/tiagoeduardobr/opencode_termux">
          <img src="https://github-readme-stats.vercel.app/api/pin/?username=tiagoeduardobr&repo=opencode_termux&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="Opencode Termux"/>
        </a>
        <br/>
        <sub>Configuração do Opencode para Termux (1 ⭐).</sub>
      </td>
      <td width="50%" align="center">
        <a href="https://github.com/tiagoeduardobr/react_native">
          <img src="https://github-readme-stats.vercel.app/api/pin/?username=tiagoeduardobr&repo=react_native&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="React Native"/>
        </a>
        <br/>
        <sub>Desenvolvimento mobile com React Native.</sub>
      </td>
    </tr>
  </table>
  ```

- [ ] **Passo 2: Adicionar badge de "Ver todos os repositórios"**

  ```markdown
  <p align="center">
    <a href="https://github.com/tiagoeduardobr?tab=repositories">
      <img src="https://img.shields.io/badge/Ver%20todos%20os%20repositórios-58a6ff?style=for-the-badge&logo=github&logoColor=white"/>
    </a>
  </p>
  ```

**Critério de aceitação:** 4 projetos em grid 2x2 com cards do github-readme-stats. Descrições breves. Links clicáveis. Layout responsivo.

---

### Task 7: Atualizar seções "Além do código", "Objetivo" e "Contato"

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1

Refinar as seções existentes com tom profissional e direto, mantendo a personalidade.

- [ ] **Passo 1: Refinar seção "Além do código"**

  ```markdown
  ## 💡 Além do código

  - 🎨 **Empreendedorismo Criativo** — Explorando a interseção entre tecnologia e trabalho artesanal/joalheria
  - 🤖 **IA + Criatividade** — Aplicando inteligência artificial em projetos criativos, como design para joias com pedras naturais
  ```

- [ ] **Passo 2: Refinar seção "Objetivo"**

  ```markdown
  ## 🎯 Objetivo

  Busco oportunidades como **Desenvolvedor Full-Stack remoto** e colaborações em projetos de e-commerce com startups no ecossistema de Santa Catarina. Aberto a desafios que unam tecnologia, performance e impacto real.
  ```

- [ ] **Passo 3: Refinar seção "Contato" com badges**

  ```markdown
  ## 📫 Contato

  <div align="center">
    <a href="https://github.com/tiagoeduardobr">
      <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white"/>
    </a>
    <a href="https://www.linkedin.com/in/tiagoeduardobr/">
      <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
    </a>
    <a href="mailto:tiago@example.com">
      <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
    </a>
  </div>
  
  <p align="center">📩 Sinta-se à vontade para enviar uma mensagem. Estou aberto a conexões e oportunidades!</p>
  ```

  > **Nota:** Substituir `tiago@example.com` pelo email real do usuário.

**Critério de aceitação:** Seções reescritas com tom profissional e direto. Badges de contato com links funcionais.

---

### Task 8: Criar GitHub Actions Workflow para atualização diária

**Arquivos:** 
- Criar: `.github/workflows/update-stats.yml`
**Complexidade:** Média
**Dependências:** Nenhuma (pode ser feito em paralelo com outras tasks)

Criar workflow que roda diariamente para manter os stats atualizados.

- [ ] **Passo 1: Criar diretório `.github/workflows/`**

  ```bash
  mkdir -p .github/workflows/
  ```

- [ ] **Passo 2: Criar workflow `update-stats.yml`**

  ```yaml
  name: Atualizar Stats do Perfil

  on:
    schedule:
      # Roda diariamente às 06:00 UTC (03:00 BRT)
      - cron: "0 6 * * *"
    workflow_dispatch:  # Permite execução manual

  jobs:
    update-readme:
      name: Atualizar README com Stats Recentes
      runs-on: ubuntu-latest
      permissions:
        contents: write
      
      steps:
        - name: Checkout do repositório
          uses: actions/checkout@v4

        - name: Atualizar README com último commit
          run: |
            # Atualiza a data da última atualização no README
            LAST_UPDATED=$(date -u "+%d/%m/%Y às %H:%M UTC")
            echo "Última atualização dos stats: $LAST_UPDATED"

        - name: Commit e Push (se houver mudanças)
          run: |
            if [[ -n "$(git status --porcelain)" ]]; then
              git config user.name "github-actions[bot]"
              git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
              git add .
              git commit -m "chore: atualizar stats do perfil [skip ci]"
              git push
            fi
  ```

- [ ] **Passo 3: Adicionar linha de "Última atualização" no README (no final do arquivo)**

  ```markdown
  ---
  <p align="center">
    <sub>Última atualização dos stats: 28/07/2026 às 21:00 UTC</sub>
    <br/>
    <sub>Gerado com ♥ por <a href="https://github.com/tiagoeduardobr/tiagoeduardobr/actions">GitHub Actions</a></sub>
  </p>
  ```

- [ ] **Passo 4: Verificar sintaxe do workflow**

  O workflow pode ser validado visualmente — a sintaxe YAML deve ser verificada contra erros comuns (indentação, espaçamento).

**Critério de aceitação:** Workflow YAML válido. Cron configurado para diário. Permissão `contents: write` para push automático. Botão "Run workflow" disponível na interface do GitHub Actions.

---

### Task 9: Adicionar rodapé e elementos decorativos finais

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1 (paleta definida)

Adicionar elementos visuais finais: snake animation, separador decorativo, rodapé consolidado.

- [ ] **Passo 1: Adicionar snake animation (contribuições)**

  ```markdown
  ## 🐍 Contribuições

  <div align="center">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/tiagoeduardobr/tiagoeduardobr/output/github-contribution-grid-snake-dark.svg" />
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/tiagoeduardobr/tiagoeduardobr/output/github-contribution-grid-snake.svg" />
      <img alt="Snake animation" src="https://raw.githubusercontent.com/tiagoeduardobr/tiagoeduardobr/output/github-contribution-grid-snake.svg" />
    </picture>
  </div>
  ```

  > **Nota:** A snake animation requer um workflow separado para gerar o SVG. Este passo é **opcional** e pode ser ativado posteriormente.

- [ ] **Passo 2: Adicionar rodapé consolidado**

  ```markdown
  ---

  <div align="center">
    <img src="https://img.shields.io/badge/Feito%20com%20%E2%9D%A4%20por-Tiago%20Eduardo-58a6ff?style=flat-square" alt="Feito com amor"/>
    <br/>
    <sub>© 2026 Tiago Eduardo Zimmermann</sub>
  </div>
  ```

**Critério de aceitação:** Rodapé com badge decorativo e copyright. Elementos visuais adicionados com elegância sem poluir o design.

---

### Task 10: Montar README completo e fazer revisão final

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Tasks 1 a 9 (todas anteriores)

Consolidar todas as seções em um README.md coeso e revisar visualmente.

- [ ] **Passo 1: Montar README completo no arquivo**

  Ordem das seções:
  1. Header / Hero (com typing SVG, badges de localização, visitas) — Task 2
  2. Sobre mim (tabela com texto + stats) — Task 3
  3. Tech Stack (4 categorias de badges) — Task 4
  4. GitHub Analytics (stats, top langs, streak, trophies, graph) — Task 5
  5. Projetos em Destaque (grid 2x2 de pinned repos) — Task 6
  6. Além do código — Task 7
  7. Objetivo — Task 7
  8. Contato (badges sociais) — Task 7
  9. Rodapé (última atualização, copyright) — Task 9

- [ ] **Passo 2: Revisar consistência visual**

  Verificar:
  - [ ] Todas as cores seguem a paleta definida na Task 1
  - [ ] Todos os badges usam `style=for-the-badge` ou `style=flat-square` consistentemente
  - [ ] Links funcionam (github, linkedin, repos)
  - [ ] Stats cards usam `theme=github_dark` ou parâmetros manuais equivalentes
  - [ ] Tabelas estão bem formatadas
  - [ ] Não há quebras de linha visíveis no GitHub
  - [ ] Contraste adequado (texto claro em fundo escuro)

- [ ] **Passo 3: Verificar preview**

  Como o README.md será renderizado no GitHub, verificar:
  - [ ] Prévia no GitHub mostra todas as seções
  - [ ] Imagens carregam (shields.io, vercel, herokuapp)
  - [ ] Links abrem corretamente
  - [ ] Layout não quebra em viewport pequena (mobile)

**Critério de aceitação:** README completo, coeso, visualmente consistente. Todas as tasks marcadas como concluídas. Preview visual aprovado.

---

## Cronograma de Implementação

| Task | Descrição | Dependência | Estimativa |
|------|-----------|------------|------------|
| 1 | Identidade visual e paleta | — | 15 min |
| 2 | Header / Hero | Task 1 | 20 min |
| 3 | Sobre Mim | Task 1 | 15 min |
| 4 | Tech Stack | Task 1 | 20 min |
| 5 | GitHub Stats | Task 1 | 25 min |
| 6 | Portfólio | Task 1 | 20 min |
| 7 | Além do código / Objetivo / Contato | Task 1 | 15 min |
| 8 | GitHub Actions Workflow | — (paralelo) | 20 min |
| 9 | Rodapé e elementos finais | Task 1 | 15 min |
| 10 | Montagem e revisão final | Tasks 1-9 | 30 min |

**Total estimado:** ~3 horas

---

## Riscos e Mitigações

| Risco | Mitigação |
|-------|-----------|
| Serviço github-readme-stats fora do ar | Cards não aparecem, mas README continua funcional. Incluir fallback textual onde possível. |
| Breaking change em badges do shields.io | Usar parâmetros estáveis (formato `for-the-badge` não deve mudar). |
| Workflow falhar por falta de permissão | Configurar `permissions: contents: write` explicitamente. |
| Cards não renderizarem no mobile | Testar com widths percentuais e `max-width=100%`. Manter layout em coluna única como fallback. |
| SVG typing effect não carregar | Header funciona sem ele — apenas perde o efeito visual. |

---

## Verificação Final

Antes de marcar como concluído:

- [ ] README.md completo com todas as seções
- [ ] `.github/workflows/update-stats.yml` criado
- [ ] Badges carregam (shields.io)
- [ ] Stats cards carregam (vercel, herokuapp)
- [ ] Links do GitHub e LinkedIn funcionam
- [ ] Paleta dark mode consistente em todo o documento
- [ ] Workflow YAML válido (sintaxe correta)
- [ ] Todos os `- [ ]` convertidos para `- [x]` com timestamp
- [ ] Preview no GitHub aprovado visualmente

---

*Plano gerado em 28/07/2026 às 21:25 UTC pelo Task Planner Agent*
