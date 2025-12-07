# Documentação da API de Gerenciamento de Tarefas

## Introdução

### Visão Geral
Esta API REST foi desenvolvida como projeto final do curso TLP1, utilizando Django REST Framework. O sistema permite gerenciar usuários, categorias e tarefas de forma completa, oferecendo operações CRUD (Create, Read, Update, Delete) para todos os recursos.

### Tecnologias Utilizadas
- **Python 3.10.3**
- **Django 5.x**
- **Django REST Framework**
- **SQLite** (banco de dados)
- **drf-yasg** (documentação interativa Swagger)

### Arquitetura
A API segue o padrão RESTful, utilizando:
- Métodos HTTP adequados (GET, POST, PUT, PATCH, DELETE)
- URLs amigáveis e previsíveis
- Formato JSON para requisições e respostas
- Códigos de status HTTP padronizados

### URL Base

http://127.0.0.1:8000/api/

text

### Documentação Interativa
Acesse a documentação Swagger em:

http://127.0.0.1:8000/api/swagger/

text

---

## Endpoints e Exemplos de Uso

### **1. Usuários**

Os usuários são os donos das tarefas no sistema. Cada usuário possui nome, email único e data de criação.

#### 1.1 Listar Todos os Usuários
**Endpoint:**

GET /api/usuarios/

text

**Descrição:** Retorna a lista completa de usuários cadastrados.

**Exemplo de Resposta (200 OK):**

[
{
"id": 1,
"nome": "João Silva",
"email": "joao@email.com",
"criado_em": "2025-12-07T18:00:00Z"
},
{
"id": 2,
"nome": "Maria Santos",
"email": "maria@email.com",
"criado_em": "2025-12-07T18:30:00Z"
}
]

text

#### 1.2 Criar Novo Usuário
**Endpoint:**

POST /api/usuarios/create/

text

**Descrição:** Cria um novo usuário no sistema.

**Headers:**

Content-Type: application/json

text

**Body (JSON):**

{
"nome": "Carlos Oliveira",
"email": "carlos@email.com"
}

text

**Exemplo de Resposta (201 CREATED):**

{
"id": 3,
"nome": "Carlos Oliveira",
"email": "carlos@email.com",
"criado_em": "2025-12-07T19:00:00Z"
}

text

**Validações:**
- O campo `nome` é obrigatório (máximo 100 caracteres)
- O campo `email` é obrigatório e deve ser único
- O email deve estar em formato válido

#### 1.3 Buscar Usuário Específico
**Endpoint:**

GET /api/usuarios/{id}/

text

**Exemplo:**

GET /api/usuarios/1/

text

**Resposta (200 OK):**

{
"id": 1,
"nome": "João Silva",
"email": "joao@email.com",
"criado_em": "2025-12-07T18:00:00Z"
}

text

**Resposta de Erro (404 NOT FOUND):**

{
"detail": "Not found."
}

text

#### 1.4 Atualizar Usuário
**Endpoint:**

PUT /api/usuarios/{id}/

text

**Body (JSON):**

{
"nome": "João Silva Atualizado",
"email": "joao.novo@email.com"
}

text

**Resposta (200 OK):**

{
"id": 1,
"nome": "João Silva Atualizado",
"email": "joao.novo@email.com",
"criado_em": "2025-12-07T18:00:00Z"
}

text

#### 1.5 Deletar Usuário
**Endpoint:**

DELETE /api/usuarios/{id}/

text

**Resposta (204 NO CONTENT):** Sem corpo na resposta.

**Nota:** Ao deletar um usuário, todas as suas tarefas também serão removidas (cascade).

---

### **2. Categorias**

Categorias são utilizadas para organizar e classificar as tarefas.

#### 2.1 Listar Todas as Categorias
**Endpoint:**

GET /api/categorias/

text

**Exemplo de Resposta (200 OK):**

[
{
"id": 1,
"nome": "Trabalho",
"descricao": "Tarefas relacionadas ao trabalho"
},
{
"id": 2,
"nome": "Pessoal",
"descricao": "Tarefas pessoais"
}
]

text

#### 2.2 Criar Nova Categoria
**Endpoint:**

POST /api/categorias/create/

text

**Body (JSON):**

{
"nome": "Urgente",
"descricao": "Tarefas de alta prioridade"
}

text

**Exemplo de Resposta (201 CREATED):**

{
"id": 3,
"nome": "Urgente",
"descricao": "Tarefas de alta prioridade"
}

text

**Validações:**
- O campo `nome` é obrigatório (máximo 50 caracteres)
- O campo `descricao` é opcional

#### 2.3 Buscar Categoria Específica
**Endpoint:**

GET /api/categorias/{id}/

text

#### 2.4 Atualizar Categoria
**Endpoint:**

PUT /api/categorias/{id}/

text

**Body (JSON):**

{
"nome": "Categoria Atualizada",
"descricao": "Nova descrição"
}

text

#### 2.5 Deletar Categoria
**Endpoint:**

DELETE /api/categorias/{id}/

text

**Resposta (204 NO CONTENT)**

---

### **3. Tarefas**

Tarefas são os itens principais do sistema, vinculados a usuários e opcionalmente a categorias.

#### 3.1 Listar Todas as Tarefas
**Endpoint:**

GET /api/tarefas/

text

**Exemplo de Resposta (200 OK):**

[
{
"id": 1,
"titulo": "Implementar API",
"status": "em_progresso",
"usuario": {
"id": 1,
"nome": "João Silva",
"email": "joao@email.com",
"criado_em": "2025-12-07T18:00:00Z"
},
"categorias": [
{
"id": 1,
"nome": "Trabalho",
"descricao": "Tarefas relacionadas ao trabalho"
}
],
"criado_em": "2025-12-07T19:00:00Z"
}
]

text

#### 3.2 Filtrar Tarefas por Status
**Endpoint:**

GET /api/tarefas/?status={status}

text

**Valores possíveis:** `pendente`, `em_progresso`, `concluida`

**Exemplo:**

GET /api/tarefas/?status=pendente

text

#### 3.3 Criar Nova Tarefa
**Endpoint:**

POST /api/tarefas/create/

text

**Body (JSON):**

{
"titulo": "Estudar Django REST Framework",
"descricao": "Aprender sobre serializers e views",
"status": "pendente",
"usuario": 1,
"categorias":

​
}

text

**Exemplo de Resposta (201 CREATED):**

{
"id": 2,
"titulo": "Estudar Django REST Framework",
"descricao": "Aprender sobre serializers e views",
"status": "pendente",
"usuario": 1,
"usuario_nome": "João Silva",
"categorias":,

​
"categorias_nomes": ["Trabalho", "Urgente"],
"criado_em": "2025-12-07T20:00:00Z",
"atualizado_em": "2025-12-07T20:00:00Z"
}

text

**Validações:**
- Campo `titulo` é obrigatório (máximo 200 caracteres)
- Campo `status` deve ser: `pendente`, `em_progresso` ou `concluida`
- Campo `usuario` é obrigatório (deve ser um ID de usuário existente)
- Campo `categorias` é opcional (aceita lista de IDs)

#### 3.4 Buscar Tarefa Específica
**Endpoint:**

GET /api/tarefas/{id}/

text

**Exemplo de Resposta (200 OK):**

{
"id": 1,
"titulo": "Implementar API",
"descricao": "Desenvolver endpoints REST",
"status": "em_progresso",
"usuario": 1,
"usuario_nome": "João Silva",
"categorias":,

​
"categorias_nomes": ["Trabalho"],
"criado_em": "2025-12-07T19:00:00Z",
"atualizado_em": "2025-12-07T19:30:00Z"
}

text

#### 3.5 Atualizar Tarefa (Completa)
**Endpoint:**

PUT /api/tarefas/{id}/

text

**Body (JSON) - Todos os campos obrigatórios:**

{
"titulo": "Implementar API - Finalizado",
"descricao": "Endpoints REST completos",
"status": "concluida",
"usuario": 1,
"categorias":

​
}

text

#### 3.6 Atualizar Tarefa (Parcial)
**Endpoint:**

PATCH /api/tarefas/{id}/

text

**Body (JSON) - Apenas campos a atualizar:**

{
"status": "concluida"
}

text

**Resposta (200 OK):**

{
"id": 1,
"titulo": "Implementar API",
"descricao": "Desenvolver endpoints REST",
"status": "concluida",
"usuario": 1,
"usuario_nome": "João Silva",
"categorias":,

​
"categorias_nomes": ["Trabalho"],
"criado_em": "2025-12-07T19:00:00Z",
"atualizado_em": "2025-12-07T21:00:00Z"
}

text

#### 3.7 Deletar Tarefa
**Endpoint:**

DELETE /api/tarefas/{id}/

text

**Resposta (204 NO CONTENT)**

---

## Códigos de Status HTTP

A API utiliza os seguintes códigos de status:

| Código | Significado | Quando Ocorre |
|--------|-------------|---------------|
| 200 | OK | Requisição bem-sucedida (GET, PUT, PATCH) |
| 201 | Created | Recurso criado com sucesso (POST) |
| 204 | No Content | Recurso deletado com sucesso (DELETE) |
| 400 | Bad Request | Dados inválidos enviados |
| 404 | Not Found | Recurso não encontrado |
| 500 | Internal Server Error | Erro no servidor |

---

## Exemplos de Uso com Postman

### Criando uma Tarefa Completa

1. **Crie um usuário:**
   - Método: POST
   - URL: `http://127.0.0.1:8000/api/usuarios/create/`
   - Body: `{"nome": "João", "email": "joao@test.com"}`

2. **Crie uma categoria:**
   - Método: POST
   - URL: `http://127.0.0.1:8000/api/categorias/create/`
   - Body: `{"nome": "Trabalho", "descricao": "Tarefas profissionais"}`

3. **Crie uma tarefa:**
   - Método: POST
   - URL: `http://127.0.0.1:8000/api/tarefas/create/`
   - Body:

{
"titulo": "Finalizar projeto",
"descricao": "Entregar documentação",
"status": "pendente",
"usuario": 1,
"categorias":

​
}

text

4. **Atualize o status:**
- Método: PATCH
- URL: `http://127.0.0.1:8000/api/tarefas/1/`
- Body: `{"status": "concluida"}`

---

## Considerações Finais

### Funcionalidades Implementadas
✅ CRUD completo para Usuários  
✅ CRUD completo para Categorias  
✅ CRUD completo para Tarefas  
✅ Relacionamento OneToMany (Usuário → Tarefas)  
✅ Relacionamento ManyToMany (Tarefa ↔ Categorias)  
✅ Filtragem de tarefas por status  
✅ Validação automática de dados  
✅ Documentação interativa Swagger  
✅ Testes automatizados  

### Testes Automatizados
A API possui cobertura de testes para os principais endpoints. Para executar os testes:

python manage.py test

text

Saída esperada:

Ran 7 tests in 0.5s
OK

text

### Melhorias Futuras
- Implementar autenticação JWT (JSON Web Tokens)
- Adicionar permissões por usuário (apenas o dono pode editar/deletar)
- Implementar paginação para listagens grandes
- Adicionar filtros avançados (data de criação, busca por texto)
- Deploy em produção (Heroku, Railway ou DigitalOcean)
- Adicionar websockets para notificações em tempo real
- Implementar sistema de notificações por email

### Estrutura do Projeto

semana17/
├── setup/
│ ├── settings.py
│ ├── urls.py
│ └── wsgi.py
├── api/
│ ├── models.py
│ ├── serializers.py
│ ├── views.py
│ ├── urls.py
│ ├── admin.py
│ └── tests.py
├── manage.py
└── db.sqlite3

text

### Como Executar o Projeto

1. **Clone ou baixe o projeto**

2. **Crie e ative o ambiente virtual:**

python -m venv venv
venv\Scripts\activate # Windows
source venv/bin/activate # Linux/Mac

text

3. **Instale as dependências:**

pip install django djangorestframework drf-yasg

text

4. **Execute as migrações:**

python manage.py makemigrations
python manage.py migrate

text

5. **Crie um superusuário (opcional):**

python manage.py createsuperuser

text

6. **Inicie o servidor:**

python manage.py runserver

text

7. **Acesse a documentação:**

http://127.0.0.1:8000/api/swagger/

text

### Contato e Suporte
- **Desenvolvedor:** [Seu Nome]
- **Email:** [seu_email@exemplo.com]
- **Repositório:** [Link do GitHub se houver]
- **Data de Desenvolvimento:** Dezembro 2025
- **Curso:** TLP1 - Técnicas de Linguagem de Programação

---

**Projeto desenvolvido como trabalho final do curso TLP1**  
**Universidade/Instituição:** [Nome da Instituição]  
**Professor:** Valdir  
**Período:** 2025.2
