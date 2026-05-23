# 📋 Kanban System JWT

Sistema de gerenciamento de tarefas no estilo **Kanban Board** com autenticação JWT, desenvolvido com **Node.js**, **Express** e frontend em **HTML/CSS/JS** puro.

---

## ✨ Funcionalidades

- **Autenticação completa** — Cadastro, login e logout com tokens JWT (validade de 8h)
- **Senhas criptografadas** — Hash com bcrypt (salt rounds: 10)
- **Revogação de tokens** — Tokens invalidados no logout são armazenados para bloqueio
- **Quadro Kanban** — 3 colunas: *A Fazer*, *Fazendo* e *Concluído*
- **Drag & Drop** — Arraste tarefas entre colunas para atualizar o status
- **CRUD de tarefas** — Criar, editar, excluir e marcar como concluída
- **Prioridades** — Baixa, Média e Alta com badges coloridos
- **Data limite** — Indicador visual de tarefas em atraso
- **Dashboard** — Contadores em tempo real (total, em andamento, concluídas, em atraso)
- **Dados por usuário** — Cada usuário visualiza apenas suas próprias tarefas
- **Design dark mode** — Interface moderna com tema escuro e fonte JetBrains Mono

---

## 🛠️ Tecnologias

| Camada     | Tecnologia                          |
|------------|-------------------------------------|
| Backend    | Node.js + Express                   |
| Auth       | JSON Web Token (JWT) + bcrypt       |
| Frontend   | HTML5, CSS3, JavaScript (Vanilla)   |
| Banco      | Arquivo JSON (file-based storage)   |
| Tipografia | JetBrains Mono (Google Fonts)       |

---

## 📁 Estrutura do Projeto

```
kanbansabado/
├── public/
│   └── index.html          # Frontend completo (HTML + CSS + JS)
├── server.js               # Servidor Express com rotas de API
├── users.json              # Dados dos usuários cadastrados
├── tasks.json              # Dados das tarefas
├── revoked_tokens.json     # Tokens JWT revogados
├── package.json            # Dependências e scripts
└── .gitignore
```

---

## 🚀 Instalação e Execução

### Pré-requisitos

- [Node.js](https://nodejs.org/) (v16 ou superior)
- npm (incluído com o Node.js)

### Passos

```bash
# 1. Clone o repositório
git clone https://github.com/motasenai122/kanbansabado.git

# 2. Acesse a pasta do projeto
cd kanbansabado

# 3. Instale as dependências
npm install

# 4. Inicie o servidor
npm start

# Ou, para desenvolvimento com hot-reload:
npm run dev
```

O servidor estará disponível em **http://localhost:3000**

---

## 📡 Endpoints da API

### Autenticação

| Método | Rota                   | Descrição              | Auth |
|--------|------------------------|------------------------|------|
| POST   | `/api/auth/register`   | Cadastrar novo usuário | ❌   |
| POST   | `/api/auth/login`      | Login (retorna JWT)    | ❌   |
| POST   | `/api/auth/logout`     | Logout (revoga token)  | ✅   |

### Tarefas (rotas protegidas)

| Método | Rota                        | Descrição                          |
|--------|-----------------------------|------------------------------------|
| GET    | `/api/tasks`                | Listar tarefas do usuário          |
| POST   | `/api/tasks`                | Criar nova tarefa                  |
| PUT    | `/api/tasks/:id`            | Editar tarefa                      |
| DELETE | `/api/tasks/:id`            | Excluir tarefa                     |
| PATCH  | `/api/tasks/:id/status`     | Atualizar status (drag & drop)     |
| PATCH  | `/api/tasks/:id/complete`   | Alternar tarefa como concluída     |

> **Nota:** Todas as rotas de tarefas exigem o header `Authorization: Bearer <token>`

---

## 📦 Dependências

| Pacote           | Versão   | Finalidade                       |
|------------------|----------|----------------------------------|
| express          | ^4.18.2  | Framework web                    |
| jsonwebtoken     | ^9.0.2   | Geração e verificação de JWT     |
| bcrypt           | ^5.1.1   | Hash de senhas                   |
| cors             | ^2.8.5   | Habilitar Cross-Origin Requests  |

---

## 📝 Licença

Este projeto é de uso acadêmico/educacional.

---

Feito com 💜 e ☕
