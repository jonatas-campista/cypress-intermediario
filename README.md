# Cypress Intermediário — testes de GUI, API e CLI no GitLab

![Cypress](https://img.shields.io/badge/Cypress-17202C?logo=cypress&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black) ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)

Suíte de testes automatizados contra uma instância local do **GitLab**, cobrindo três camadas:
interface gráfica, API REST e linha de comando. Desenvolvida durante o curso de Cypress (intermediário)
da Escola TAT.

## O que é testado

| Camada | Testes |
|---|---|
| **GUI** | login, logout, criar projeto, criar issue, adicionar label e milestone a uma issue |
| **API** | criar projeto e criar issue via API v4, com autenticação por token |
| **CLI** | `git clone` de um projeto criado pelos testes, usando `cy.exec` |

## Técnicas usadas

- **Comandos customizados separados por camada** (`gui_commands.js`, `api_commands.js`, `cli_commands.js`).
- **Pré-condições pela API**: o projeto e a issue são criados via API antes do teste de GUI, que testa
  só a ação de interesse. Os testes ficam mais rápidos e menos frágeis.
- **Limpeza do ambiente** antes de cada teste (exclusão dos projetos via API).
- **Sessão em cache** com `cy.session` para não repetir o login.
- **Dados dinâmicos** com Faker, evitando conflito entre execuções.
- **Dados sensíveis** (senha e token) fora do código, em `cypress.env.json`.

## Como rodar

**Pré-requisitos:** Node.js, Docker e uma instância do GitLab rodando localmente (o roteiro de
configuração está em [`lessons/`](lessons/)).

```bash
npm install

# crie cypress.env.json com user_password e gitlab_access_token
npx cypress run     # headless
npx cypress open    # interativo
```

## Créditos

Baseado no curso [Testes automatizados com Cypress (intermediário)](https://github.com/wlsf82/cypress-intermediario-v2),
de Walmyr Filho (Escola TAT). Os testes e comandos deste repositório foram escritos por mim durante o curso.
