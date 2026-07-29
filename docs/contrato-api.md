# Contrato da API — OrbitBoard

## 1. Informações gerais

- **Base URL:** `http://localhost:5200`
- **Formato de envio e resposta:** JSON
- **Documentação interativa:** `http://localhost:5200/swagger`

## 2. Health check

### GET `/health`

Verifica se a API está disponível.

Exemplo de resposta:

```json
{
  "status": "healthy",
  "service": "OrbitBoard.Api",
  "utcTime": "2026-07-29T18:07:24.666329+00:00"
}
```

## 3. Dashboard

### GET `/api/dashboard`

Retorna os indicadores consolidados da aplicação, incluindo quantidade de projetos, tarefas, concluídas, atrasadas e distribuição por status.

## 4. Projetos

### GET `/api/projects`

Lista todos os projetos.

### GET `/api/projects/{id}`

Retorna um projeto pelo identificador.

### POST `/api/projects`

Cria um projeto.

### PUT `/api/projects/{id}`

Atualiza um projeto existente.

### DELETE `/api/projects/{id}`

Exclui um projeto.

## 5. Tarefas

### GET `/api/tasks`

Lista tarefas e permite filtros conforme os parâmetros disponibilizados pela API.

### GET `/api/tasks/{id}`

Retorna uma tarefa pelo identificador.

### POST `/api/tasks`

Cria uma tarefa.

### PUT `/api/tasks/{id}`

Atualiza os dados de uma tarefa.

### PATCH `/api/tasks/{id}/status`

Altera somente o status da tarefa.

### DELETE `/api/tasks/{id}`

Exclui uma tarefa.

## 6. Equipe

### GET `/api/team-members`

Lista os integrantes disponíveis para associação às tarefas e aos projetos.

## 7. Códigos de resposta esperados

| Código | Significado |
|---:|---|
| 200 | Requisição processada com sucesso |
| 201 | Recurso criado com sucesso |
| 204 | Operação concluída sem conteúdo de resposta |
| 400 | Dados inválidos enviados pelo cliente |
| 404 | Recurso não encontrado |
| 500 | Erro interno tratado pela API |

## 8. Tratamento de erros

A API possui middleware global para capturar exceções e devolver respostas padronizadas, evitando que erros internos sejam expostos diretamente ao usuário.

## 9. Observação

Os modelos completos de requisição e resposta podem ser consultados e testados diretamente no Swagger da aplicação.
