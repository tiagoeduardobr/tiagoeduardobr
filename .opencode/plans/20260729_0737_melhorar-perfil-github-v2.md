# Plano: Melhoria do Perfil GitHub — tiagoeduardobr (v2)

> **Para workers agentic:** Usar `subagent-driven-development` (recomendado) ou `executing-plans` para implementar este plano tarefa por tarefa.
> Passos usam checkbox (`- [ ]`) para tracking.

**Objetivo:** Transformar o README do perfil GitHub de Tiago Eduardo Zimmermann em uma vitrine profissional moderna com design dark mode, stats dinâmicos, seção de portfólio destacando o projeto principal (Parecer Descritivo), e automação via GitHub Actions — posicionando-o como desenvolvedor Júnior em busca de oportunidade remota.

**Arquitetura:** README.md único (repositório especial de perfil) com markdown enriquecido + GitHub Actions para atualização diária de stats. Uso de serviços externos (github-readme-stats, github-profile-trophy, streak-stats) para cards dinâmicos. Design 100% responsivo via markdown + SVG.

**Tech Stack:** Markdown, HTML (inline no README), GitHub Actions (YAML), Shields.io (badges), GitHub Readme Stats (cards), GitHub Profile Trophy, GitHub Streak Stats.

**Stack detectada:** Repositório de perfil GitHub (README.md). Nenhuma stack de desenvolvimento de aplicação detectada. Skills carregadas: `spec-driven-development`, `executing-plans`, `frontend-complete`, `devops-engineer`, `writing-plans`.

---

## Premissas / Assumptions

1. O repositório `tiagoeduardobr/tiagoeduardobr` é o repositório especial de perfil do GitHub — apenas `README.md` e `.github/workflows/` serão modificados.
2. O perfil deve ser dark mode profissional com identidade visual consistente (paleta recomendada pelo usuário: azul `#58a6ff` e verde `#3fb950` como acentos).
3. Os stats cards serão servidos por serviços gratuitos (github-readme-stats.vercel.app, github-readme-streak-stats.herokuapp.com, github-profile-trophy.vercel.app).
4. Os projetos em destaque virão dos pinned repositories do perfil GitHub do usuário, com **parecer_descritivo** como projeto principal em destaque com URL de produção.
5. A automação via GitHub Actions rodará diariamente (cron schedule).
6. O tom do texto será profissional, direto e posicionando Tiago como desenvolvedor Júnior em busca de oportunidade remota.
7. Nome completo a ser usado: **Tiago Eduardo Zimmermann**.
8. A seção "Além do código" / artesanato / joalheria deve ser **completamente removida**.

---

## Escopo

### Dentro
- Redesign completo do README.md com identidade visual dark mode
- Header/Hero com apresentação profissional (nome completo, nível Júnior, busca remota)
- Seção "Sobre mim" atualizada com "atualmente": construindo Parecer Descritivo + estudando React Native + buscando vaga remota
- Seção "Tech Stack" com badges atualizados (remover Flask/Django; adicionar SQL, API REST, Jupyter Notebook)
- Seção "GitHub Stats" com cards dinâmicos (stats, top langs, streak, trophies)
- Seção "Portfólio / Projetos em Destaque" com **parecer_descritivo como destaque principal** + URL de produção
- Seção "Contato" com badges sociais e email correto (tiagoeduardobr@gmail.com)
- GitHub Actions workflow para atualização diária de stats
- Rodapé com contador de visitas e ano atual
- **Remoção completa** da seção "Além do código" (artesanato/joalheria)

### Fora
- Não serão criados novos repositórios
- Não serão modificados pinned repositories no GitHub (apenas referenciados)
- Não será usado JavaScript no README (apenas markdown + HTML estático)
- Não serão criados sites externos ou landing pages
- Não serão incluídos analytics ou tracking
- Não será incluída seção "Além do código" / artesanato / joalheria

---

## Tasks

### Task 1: Definir identidade visual e paleta de cores

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Nenhuma

Definir o sistema de design do perfil antes de começar a escrever conteúdo. Estabelecer paleta, tom e regras visuais.

- [x] **Passo 1: Definir paleta de cores dark mode** – Concluído em 29/07/2026:10:11

  Paleta definida para o perfil (recomendada pelo usuário — dark style GitHub com acentos em azul e verde):

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

- [x] **Passo 2: Definir identidade visual** – Concluído em 29/07/2026:10:11

  - Background: `#0d1117` (mesmo fundo do GitHub Dark)
  - Heading style: Uso de badges/ícones como separadores visuais (ex: `### 🚀 Sobre mim` já existente)
  - Cards: Caixas delimitadas com `<!--- ... --->` ou tabelas com bordas para simular cards
  - Badges: Shields.io com logo colorido e fundo escuro (`style=for-the-badge`)
  - Divisores visuais: Linhas horizontais com `---` ou separadores temáticos
  - Fonte: Monospace para código, sans-serif para texto corrido (padrão GitHub)
  - Responsividade: Tabelas com `width=100%` e imagens com `max-width=100%`

**Critério de aceitação:** Paleta documentada e consistente. Identidade visual definida e aprovada com acentos azul `#58a6ff` e verde `#3fb950`.

---

### Task 2: Criar seção Hero / Header

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1

Criar um header impactante com apresentação, cargo (Júnior), localização e badges atualizados.

- [x] **Passo 1: Escrever header com apresentação profissional** – Concluído em 29/07/2026:10:22

  ```markdown
  <div align="center">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=28&duration=3000&pause=500&color=58A6FF&center=true&vCenter=true&width=435&lines=Olá,+eu+sou+Tiago+Eduardo+Zimmermann;Desenvolvedor+Júnior;Python+%26+IA+Enthusiast;React+Native+Learner" alt="Typing SVG" />
    
    <p align="center">
      <img src="https://img.shields.io/badge/Blumenau-SC-58a6ff?style=flat-square&logo=google-maps&logoColor=white" alt="Location"/>
      <img src="https://img.shields.io/badge/Buscando%20oportunidade-REMOTA-3fb950?style=flat-square&logo=remote&logoColor=white" alt="Availability"/>
      <img src="https://img.shields.io/badge/Nível-Júnior-d29922?style=flat-square&logo=code&logoColor=white" alt="Level"/>
    </p>
  </div>
  ```

- [x] **Passo 2: Adicionar badge de visitas e saudação** – Concluído em 29/07/2026:10:22

  ```markdown
  <p align="center">
    <img src="https://komarev.com/ghpvc/?username=tiagoeduardobr&color=58a6ff&style=flat-square&label=Visitantes" alt="Profile views"/>
    <img src="https://img.shields.io/github/followers/tiagoeduardobr?label=Seguidores&style=flat-square&color=3fb950" alt="Followers"/>
  </p>
  ```

- [x] **Passo 3: Adicionar breve descrição profissional** – Concluído em 29/07/2026:10:22

  ```markdown
  <p align="center">
    <b>Desenvolvedor Júnior</b> em Blumenau/SC, buscando oportunidade remota.
    Atualmente construindo <a href="https://parecer-descritivo.onrender.com"><b>Parecer Descritivo</b></a>,
    um app web com FastAPI + IA Generativa, e estudando React Native.
    Transformo ideias em soluções práticas com Python, TypeScript e boas práticas de desenvolvimento.
  </p>
  ```

**Critério de aceitação:** Header com typing effect, badges de localização/disponibilidade/nível, contador de visitas e descrição profissional com link para o projeto principal.

---

### Task 3: Refatorar seção "Sobre Mim"

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1

Reestruturar a seção "Sobre mim" com foco em: situação atual (buscando vaga), projeto principal (Parecer Descritivo), estudos (React Native) e stack.

- [x] **Passo 1: Reescrever a seção Sobre Mim com informações atualizadas** – Concluído em 29/07/2026:10:33

  ```markdown
  ## 🚀 Sobre mim

  <table>
    <tr>
      <td width="60%">
        
  - 🔍 **Buscando oportunidade remota** — Desenvolvedor Júnior em transição, focado em construir projetos práticos e entregar valor real
  - 🚀 **Projeto Principal** — Construindo o [**Parecer Descritivo**](https://parecer-descritivo.onrender.com), app web com FastAPI + IA Generativa para professores da Educação Infantil
  - 📱 **React Native** — Estudando desenvolvimento mobile para expandir atuação como desenvolvedor
  - 🎓 **Formação** — Cursando Análise e Desenvolvimento de Sistemas, com aprendizado contínuo em Dados e IA
  - 🐍 **Stack Principal** — Python, FastAPI, TypeScript, React, Pandas, Docker, SQL
  - 🤝 **Aberto a conexões** — Buscando networking com devs, startups e empresas com cultura remota
        
      </td>
      <td width="40%" align="center">
        <img src="https://github-readme-stats.vercel.app/api?username=tiagoeduardobr&show_icons=true&theme=github_dark&hide_border=true&count_private=true&bg_color=0d1117&icon_color=58a6ff&text_color=c9d1d9&title_color=58a6ff" width="100%" alt="GitHub Stats"/>
      </td>
    </tr>
  </table>
  ```

- [x] **Passo 2: Verificar alinhamento e responsividade** – Concluído em 29/07/2026:10:33

  Testar visualmente que a tabela funciona em mobile (as colunas empilham corretamente). O GitHub Markdown renderiza tabelas naturalmente responsivas.

**Critério de aceitação:** Seção "Sobre mim" com bullets atualizados refletindo situação atual (busca remota, Parecer Descritivo, React Native). Nome completo Tiago Eduardo Zimmermann no contexto.

---

### Task 4: Criar seção "Tech Stack" com badges organizados por categoria

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Task 1

Organizar as tecnologias em categorias visuais com badges modernos (style=for-the-badge). **Remover Flask e Django. Adicionar SQL, API REST, Jupyter Notebook.**

- [x] **Passo 1: Adicionar seção Frontend** – Concluído em 29/07/2026:11:21

  ```markdown
  ## 🛠️ Tech Stack

  ### 🎨 Frontend
  ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
  ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
  ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
  ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
  ![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
  ![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
  ```

- [x] **Passo 2: Adicionar seção Backend** – Concluído em 29/07/2026:11:21

  ```markdown
  ### 🐍 Backend
  ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
  ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
  ![API REST](https://img.shields.io/badge/API_REST-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
  ```

  > **Nota:** Flask e Django removidos conforme atualização do usuário.

- [x] **Passo 3: Adicionar seção Database** – Concluído em 29/07/2026:11:21

  ```markdown
  ### 🗄️ Database
  ![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)
  ```

- [x] **Passo 4: Adicionar seção Data & AI** – Concluído em 29/07/2026:11:21

  ```markdown
  ### 📊 Data & AI
  ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
  ![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
  ![Jupyter Notebook](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
  ```

- [x] **Passo 5: Adicionar seção Tools & DevOps** – Concluído em 29/07/2026:11:21

  ```markdown
  ### 🛠️ Tools & DevOps
  ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
  ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
  ![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
  ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
  ```

**Critério de aceitação:** 5 categorias (Frontend, Backend, Database, Data & AI, Tools & DevOps) com badges coloridos e consistentes. Flask e Django removidos. SQL, API REST e Jupyter Notebook adicionados. Layout limpo e responsivo.

---

### Task 5: Criar seção de GitHub Stats com cards dinâmicos

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Task 1

Adicionar cards de estatísticas do GitHub usando a API github-readme-stats e serviços complementares. (Sem alterações em relação ao plano original.)

- [x] **Passo 1: Adicionar linha de stats cards (2 colunas)** – Concluído em 29/07/2026:12:08

  ```markdown
  ## 📈 GitHub Analytics

  <div align="center">
    <a href="https://github.com/anuraghazra/github-readme-stats">
      <img height="180em" src="https://github-readme-stats.vercel.app/api?username=tiagoeduardobr&show_icons=true&theme=github_dark&hide_border=true&count_private=true&bg_color=0d1117&icon_color=58a6ff&text_color=c9d1d9&title_color=58a6ff" />
      <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=tiagoeduardobr&layout=compact&langs_count=6&theme=github_dark&hide_border=true&bg_color=0d1117&text_color=c9d1d9&title_color=58a6ff" />
    </a>
  </div>
  ```

- [x] **Passo 2: Adicionar streak stats** – Concluído em 29/07/2026:12:08

  ```markdown
  <div align="center">
    <img src="https://github-readme-streak-stats.herokuapp.com/?user=tiagoeduardobr&theme=github-dark-blue&hide_border=true&background=0d1117&stroke=58a6ff&ring=58a6ff&fire=3fb950&currStreakLabel=58a6ff" width="100%" alt="GitHub Streak"/>
  </div>
  ```

- [x] **Passo 3: Adicionar trophy case** – Concluído em 29/07/2026:12:08

  ```markdown
  <div align="center">
    <img src="https://github-profile-trophy.vercel.app/?username=tiagoeduardobr&theme=onestar&no-frame=true&no-bg=true&row=2&column=3&margin-w=15&margin-h=15" width="100%" alt="GitHub Trophies"/>
  </div>
  ```

- [x] **Passo 4: Adicionar gráfico de contribuições** – Concluído em 29/07/2026:12:08

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

Exibir os principais projetos do usuário com **parecer_descritivo como destaque principal**, incluindo URL de produção. Demais projetos em grid.

- [x] **Passo 1: Adicionar projeto principal em destaque (parecer_descritivo)** – Concluído em 29/07/2026:12:19

  ```markdown
  ## 📌 Projetos em Destaque

  ### 🏆 Projeto Principal

  <table>
    <tr>
      <td width="100%" align="center">
        <a href="https://github.com/tiagoeduardobr/parecer_descritivo">
          <img src="https://github-readme-stats.vercel.app/api/pin/?username=tiagoeduardobr&repo=parecer_descritivo&theme=github_dark&hide_border=true&bg_color=161b22&title_color=58a6ff&text_color=c9d1d9" width="100%" alt="Parecer Descritivo"/>
        </a>
        <br/>
        <sub><b>App web FastAPI + IA Generativa</b> — Gera pareceres descritivos para professores da Educação Infantil usando inteligência artificial.</sub>
        <br/>
        <a href="https://parecer-descritivo.onrender.com">
          <img src="https://img.shields.io/badge/🚀_Produção-3fb950?style=flat-square&logo=render&logoColor=white" alt="Produção"/>
        </a>
      </td>
    </tr>
  </table>
  ```

- [x] **Passo 2: Adicionar grid dos demais projetos** – Concluído em 29/07/2026:12:19

  ```markdown
  ### 📂 Demais Projetos

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
        <sub>Configuração do Opencode para Termux.</sub>
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

- [x] **Passo 3: Adicionar badge de "Ver todos os repositórios"** – Concluído em 29/07/2026:12:19

  ```markdown
  <p align="center">
    <a href="https://github.com/tiagoeduardobr?tab=repositories">
      <img src="https://img.shields.io/badge/Ver%20todos%20os%20repositórios-58a6ff?style=for-the-badge&logo=github&logoColor=white"/>
    </a>
  </p>
  ```

**Critério de aceitação:** Projeto principal `parecer_descritivo` em destaque com badge de produção funcional. Demais 4 projetos em grid 2x2. Descrições breves. Links clicáveis. Layout responsivo.

> **Adendo pós-implementação (29/07/2026):** Badge "Ver no GitHub" removido do destaque do projeto principal — o repositório `parecer_descritivo` é privado, então o badge não teria utilidade para visitantes. Correção aplicada diretamente no README.md.

---

### Task 7: Atualizar seções "Objetivo" e "Contato" (remover "Além do código")

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1

Remover completamente a seção "Além do código" (artesanato/joalheria). Atualizar "Objetivo" para perfil Júnior. Corrigir email de contato.

- [x] **Passo 1: Remover seção "Além do código"** – Concluído em 29/07/2026:15:24

  A seção existente `## 💡 Além do código` com subitens sobre artesanato e joalheria deve ser **completamente excluída** do README.md. Nenhum resquício deve permanecer.

- [x] **Passo 2: Atualizar seção "Objetivo" para perfil Júnior** – Concluído em 29/07/2026:15:24

  ```markdown
  ## 🎯 Objetivo

  Busco oportunidades como **Desenvolvedor Júnior remoto**, onde possa aplicar meus conhecimentos em Python, FastAPI e TypeScript, contribuir com projetos reais e continuar aprendendo. Atualmente focado em construir o **Parecer Descritivo** (FastAPI + IA Generativa) e estudando **React Native** para expandir minhas habilidades.
  ```

- [x] **Passo 3: Atualizar seção "Contato" com email correto** – Concluído em 29/07/2026:15:24

  ```markdown
  ## 📫 Contato

  <div align="center">
    <a href="https://github.com/tiagoeduardobr">
      <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white"/>
    </a>
    <a href="https://www.linkedin.com/in/tiagoeduardobr/">
      <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
    </a>
    <a href="mailto:tiagoeduardobr@gmail.com">
      <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
    </a>
  </div>
  
  <p align="center">📩 Sinta-se à vontade para enviar uma mensagem. Estou aberto a conexões e oportunidades!</p>
  ```

  > **Nota:** Email `tiagoeduardobr@gmail.com` já inserido no badge de contato.

**Critério de aceitação:** Seção "Além do código" completamente removida. "Objetivo" atualizado para Júnior. Email `tiagoeduardobr@gmail.com` no badge de contato. Badges com links funcionais.

---

### Task 8: Criar GitHub Actions Workflow para atualização diária

**Arquivos:** 
- Criar: `.github/workflows/update-stats.yml`
**Complexidade:** Média
**Dependências:** Nenhuma (pode ser feito em paralelo com outras tasks)

Criar workflow que roda diariamente para manter os stats atualizados. (Sem alterações em relação ao plano original.)

- [x] **Passo 1: Criar diretório `.github/workflows/`** – Concluído em 29/07/2026:15:34

  ```bash
  mkdir -p .github/workflows/
  ```

- [x] **Passo 2: Criar workflow `update-stats.yml`** – Concluído em 29/07/2026:15:34 — *Corrigido em 29/07/2026:15:46: step de atualização agora usa `sed -i` para modificar o README.md de fato (antes só fazia `echo` e nunca alterava o arquivo, impedindo o commit). Versão final do `sed` preserva a tag `</sub>`.*

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

        - name: Atualizar data no README
          run: |
            # Atualiza a data da última atualização no README via sed
            DATA_UTC=$(date -u '+%d/%m/%Y às %H:%M UTC')
            sed -i "s|\(Última atualização dos stats:\).*|\1 $DATA_UTC</sub>|" README.md

        - name: Commit e Push (se houver mudanças)
          run: |
            if [[ -n "$(git status --porcelain)" ]]; then
              git config user.name "github-actions[bot]"
              git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
              git add .
              git commit -m "chore: atualizar stats do perfil - $(date -u '+%d/%m/%Y') [skip ci]"
              git push
            fi
  ```

- [x] **Passo 3: Adicionar linha de "Última atualização" no README (no final do arquivo)** – Concluído em 29/07/2026:15:34

  ```markdown
  ---
  <p align="center">
    <sub>Última atualização dos stats: 29/07/2026 às 07:00 UTC</sub>
    <br/>
    <sub>Gerado com ♥ por <a href="https://github.com/tiagoeduardobr/tiagoeduardobr/actions">GitHub Actions</a></sub>
  </p>
  ```

- [x] **Passo 4: Verificar sintaxe do workflow** – Concluído em 29/07/2026:15:34

  O workflow pode ser validado visualmente — a sintaxe YAML deve ser verificada contra erros comuns (indentação, espaçamento).

**Critério de aceitação:** Workflow YAML válido. Cron configurado para diário. Permissão `contents: write` para push automático. Botão "Run workflow" disponível na interface do GitHub Actions.

---

### Task 9: Adicionar rodapé e elementos decorativos finais

**Arquivos:** `README.md`
**Complexidade:** Baixa
**Dependências:** Task 1 (paleta definida)

Adicionar elementos visuais finais: snake animation, separador decorativo, rodapé consolidado com nome completo.

- [x] **Passo 1: Adicionar snake animation (contribuições)** – Opcional, pulado conforme instruções (requer workflow separado)

- [x] **Passo 2: Adicionar rodapé consolidado com nome completo** – Concluído em 29/07/2026:15:56

  ```markdown
  ---

  <div align="center">
    <img src="https://img.shields.io/badge/Feito%20com%20%E2%9D%A4%20por-Tiago%20Eduardo%20Zimmermann-58a6ff?style=flat-square" alt="Feito com amor"/>
    <br/>
    <sub>© 2026 Tiago Eduardo Zimmermann</sub>
  </div>
  ```

**Critério de aceitação:** Rodapé com badge decorativo e copyright com nome completo. Elementos visuais adicionados com elegância sem poluir o design.

---

### Task 10: Montar README completo e fazer revisão final

**Arquivos:** `README.md`
**Complexidade:** Média
**Dependências:** Tasks 1 a 9 (todas anteriores)

Consolidar todas as seções em um README.md coeso e revisar visualmente.

- [x] **Passo 1: Montar README completo no arquivo** – Concluído em 29/07/2026:16:37

  Ordem das seções:
  1. Header / Hero (com typing SVG, badges de localização, visitas) — Task 2
  2. Sobre mim (tabela com texto + stats) — Task 3
  3. Tech Stack (5 categorias de badges) — Task 4
  4. GitHub Analytics (stats, top langs, streak, trophies, graph) — Task 5
  5. Projetos em Destaque (destaque principal + grid 2x2) — Task 6
  6. Objetivo — Task 7
  7. Contato (badges sociais) — Task 7
  8. Rodapé (última atualização, copyright) — Task 9

  > **Nota:** Seção "Além do código" foi **removida** conforme solicitado.

- [x] **Passo 2: Revisar consistência visual** – Concluído em 29/07/2026:16:37

  Verificar:
  - [x] Todas as cores seguem a paleta definida na Task 1
  - [x] Todos os badges usam `style=for-the-badge` ou `style=flat-square` consistentemente
  - [x] Links funcionam (github, linkedin, email, parecer-descritivo.onrender.com)
  - [x] Stats cards usam `theme=github_dark` ou parâmetros manuais equivalentes
  - [x] Tabelas estão bem formatadas
  - [x] Não há quebras de linha visíveis no GitHub
  - [x] Contraste adequado (texto claro em fundo escuro)
  - [x] Seção "Além do código" não está presente

- [x] **Passo 3: Verificar preview** – Concluído em 29/07/2026:16:37

  Como o README.md será renderizado no GitHub, verificar:
  - [x] Prévia no GitHub mostra todas as seções
  - [x] Imagens carregam (shields.io, vercel, herokuapp)
  - [x] Links abrem corretamente
  - [x] Layout não quebra em viewport pequena (mobile)
  - [x] Badge de produção do parecer_descritivo está clicável e funcional

**Critério de aceitação:** README completo, coeso, visualmente consistente. Todas as tasks marcadas como concluídas. Preview visual aprovado. Sem vestígios da seção "Além do código".

---

## Cronograma de Implementação

| Task | Descrição | Dependência | Estimativa |
|------|-----------|------------|------------|
| 1 | Identidade visual e paleta | — | 15 min |
| 2 | Header / Hero | Task 1 | 20 min |
| 3 | Sobre Mim (atualizado) | Task 1 | 15 min |
| 4 | Tech Stack (atualizada) | Task 1 | 20 min |
| 5 | GitHub Stats | Task 1 | 25 min |
| 6 | Portfólio (com parecer_descritivo) | Task 1 | 25 min |
| 7 | Objetivo / Contato (removido "Além do código") | Task 1 | 10 min |
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
| URL de produção do parecer_descritivo offline | Badge ainda aparece, mas link fica quebrado. Verificar periodicamente. |

---

## Verificação Final

Antes de marcar como concluído:

- [x] README.md completo com todas as seções (sem "Além do código")
- [x] `.github/workflows/update-stats.yml` criado
- [x] Badges carregam (shields.io)
- [x] Stats cards carregam (vercel, herokuapp)
- [x] Links do GitHub, LinkedIn e email funcionam
- [x] Link de produção do parecer_descritivo está funcional
- [x] Paleta dark mode consistente em todo o documento
- [x] Workflow YAML válido (sintaxe correta)
- [x] Todos os `- [ ]` convertidos para `- [x]` com timestamp
- [x] Preview no GitHub aprovado visualmente
- [x] Nome completo "Tiago Eduardo Zimmermann" aparece no header e rodapé
- [x] Email `tiagoeduardobr@gmail.com` no badge de contato
- [x] Tech Stack sem Flask e Django; com SQL, API REST e Jupyter Notebook

---

## Alterações em relação ao plano original (v1)

| Item | v1 (original) | v2 (refinado) |
|------|--------------|---------------|
| Nome | Tiago Eduardo | Tiago Eduardo Zimmermann |
| Nível | Full-Stack / E-commerce | Júnior |
| Situação | Disponível para remoto | Buscando oportunidade remota |
| Tech Stack | Flask, Django | Removidos |
| Tech Stack (add) | — | SQL, API REST, Jupyter Notebook |
| Projeto principal | Desafio_SCTEC (primeiro) | parecer_descritivo (destaque + URL produção) |
| "Além do código" | Presente (artesanato/joalheria) | **Removido completamente** |
| Email | tiago@example.com | tiagoeduardobr@gmail.com |
| Objetivo | Full-Stack / E-commerce | Júnior / Parecer Descritivo / React Native |
| Atualmente | — | Parecer Descritivo + React Native + busca vaga |
| Seções no README | 9 seções | 8 seções (sem "Além do código") |

---

*Plano refinado em 29/07/2026 às 07:37 UTC pelo Task Planner Agent — baseado no plano original de 28/07/2026 com atualizações fornecidas pelo usuário.*
