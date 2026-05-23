# 🚀 Dossiê de Deploy: Kanban System JWT na Render

Este guia descreve todas as configurações e modificações realizadas no projeto para viabilizar um deploy estável e de sucesso na plataforma **Render**, além do passo a passo completo para sua configuração.

---

## 🛠️ 1. Ajustes Realizados no Projeto

Para garantir que o projeto funcione tanto localmente quanto em nuvem na Render de maneira automática, realizamos as seguintes alterações:

### 🔹 Servidor Express (`server.js`)
* **Porta Dinâmica**: Substituímos a porta estática `3000` por `process.env.PORT || 3000`. A Render define automaticamente a variável `PORT` na máquina virtual onde o app roda.
* **Segurança de Tokens**: A chave JWT agora busca `process.env.JWT_SECRET` em produção, mantendo a chave padrão apenas como fallback local.

### 🔹 Interface Frontend (`public/index.html`)
* **URL Relativa da API**: Alteramos `const API_URL = 'http://localhost:3000/api';` para `const API_URL = '/api';`. Como o backend Express serve o frontend estaticamente pela rota padrão, o uso de rotas relativas permite que as chamadas de API funcionem instantaneamente em qualquer domínio (seja no `localhost` ou no domínio gerado pela Render) sem necessidade de alterar códigos.

---

## 💾 2. Nota Crítica sobre Armazenamento (Banco de Dados JSON)

Este projeto utiliza armazenamento baseado em arquivos (`users.json`, `tasks.json`, `revoked_tokens.json`). 

> [!WARNING]
> **Atenção sobre o Plano Gratuito (Free) da Render**:
> Por padrão, instâncias gratuitas da Render possuem **sistemas de arquivos efêmeros**. Isso significa que toda vez que a aplicação reiniciar (após ficar inativa por 15 minutos ou ao realizar um novo deploy), as tarefas e usuários cadastrados **serão reiniciados para o estado original enviado ao GitHub**.
> 
> **Como resolver para manter os dados persistentes?**
> * **Opção A (Recomendada/Produção)**: Substituir o sistema de arquivos por um banco de dados real hospedado (como Supabase ou MongoDB Atlas).
> * **Opção B (Render Disks)**: No plano pago da Render, você pode associar um **Render Disk** montado em `/usr/src/app/data` e atualizar os caminhos no `server.js` para apontar os arquivos `.json` para lá.

---

## 📋 3. Passo a Passo Completo para Deploy na Render

Siga as etapas abaixo para colocar o seu Kanban no ar:

### Passo 1: Acessar a Render
1. Vá para [render.com](https://render.com/) e faça login (recomendado conectar com sua conta do GitHub).

### Passo 2: Criar um Novo Serviço
1. Clique no botão **New +** no canto superior direito.
2. Selecione a opção **Web Service**.

### Passo 3: Conectar seu Repositório
1. Na lista de repositórios do seu GitHub conectado, busque por:
   **`kanbansabadoagoravai`**
2. Clique no botão **Connect** ao lado do repositório.

### Passo 4: Configurações do Web Service
Preencha os campos conforme as instruções abaixo:

* **Name**: `kanban-jwt-sabado` (ou o nome de sua preferência)
* **Region**: Escolha uma região próxima (ex: *Ohio (us-east-2)* ou *Frankfurt (eu-central-1)*)
* **Branch**: `main`
* **Runtime**: `Node`
* **Build Command**: `npm install`
* **Start Command**: `npm start`
* **Instance Type**: Escolha o plano **Free** (ou o de sua preferência)

### Passo 5: Adicionar Variáveis de Ambiente (Crucial)
1. Clique na aba/seção **Advanced**.
2. Clique em **Add Environment Variable**.
3. Adicione a seguinte variável:
   * **Key**: `JWT_SECRET`
   * **Value**: Crie uma chave secreta forte (ex: `UmaChaveSuperSecretaEDificilDeQuebrar123!`)
4. Clique em **Save**.

### Passo 6: Acompanhar o Deploy
1. A Render iniciará o processo de build automaticamente.
2. Acompanhe os logs no console da Render. Você deverá ver o progresso do `npm install` e a mensagem:
   `Server running on http://localhost:10000` (ou outra porta interna).
3. Uma vez concluído com sucesso, o status mudará para **Live** (verde).
4. O link público do seu Kanban estará no topo da tela, geralmente no formato: 
   `https://kanban-jwt-sabado.onrender.com`

---

## 🧪 4. Como Testar
Abra a URL gerada no seu navegador:
1. Registre uma nova conta na tela de registro.
2. Faça login para acessar o quadro Kanban.
3. Crie tarefas, mova-as de coluna (drag & drop), alterne o status de conclusão e verifique os contadores do dashboard. Tudo funcionará de forma otimizada e integrada na nuvem!
