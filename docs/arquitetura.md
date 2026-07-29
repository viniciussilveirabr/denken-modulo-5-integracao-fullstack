# Arquitetura da Aplicação — OrbitBoard

## 1. Visão geral

O OrbitBoard é uma aplicação full stack didática para gerenciamento de projetos, tarefas e equipe. A solução foi organizada em duas aplicações independentes, integradas por chamadas HTTP com dados em JSON:

- **Front-end:** React com Vite.
- **Back-end:** ASP.NET Core .NET 8.
- **Servidor web do front-end:** Nginx.
- **Dados:** mantidos em memória pela API.
- **Infraestrutura:** Docker e Docker Compose.

## 2. Fluxo da aplicação

1. O usuário acessa o front-end pelo navegador.
2. O React envia requisições HTTP para a API.
3. A API executa as regras do serviço e manipula os dados em memória.
4. O back-end retorna respostas em JSON.
5. O front-end atualiza a interface conforme o resultado da requisição.

```text
Navegador
   |
   | HTTP/JSON
   v
Front-end React + Nginx
   |
   | HTTP/JSON
   v
Back-end ASP.NET Core
   |
   v
Dados em memória
```

## 3. Front-end

O front-end é responsável por:

- exibir o dashboard;
- listar projetos, tarefas e integrantes;
- enviar dados de formulários para a API;
- apresentar estados de carregamento, sucesso e erro;
- atualizar a interface após operações realizadas.

### Tecnologias

- React
- Vite
- JavaScript
- CSS
- Nginx

### Porta

```text
http://localhost:5173
```

## 4. Back-end

O back-end é responsável por:

- disponibilizar a API REST;
- receber e validar requisições;
- executar operações de projetos e tarefas;
- retornar respostas em JSON;
- disponibilizar documentação pelo Swagger;
- tratar erros por middleware global.

### Tecnologias

- ASP.NET Core .NET 8
- C#
- Swagger/OpenAPI
- Injeção de dependência
- Middleware de tratamento de erros

### Porta

```text
http://localhost:5200
```

## 5. CORS

A API permite a origem do front-end executado em:

```text
http://localhost:5173
```

Essa configuração permite que o navegador aceite a comunicação entre aplicações executadas em portas diferentes.

## 6. Docker

Cada aplicação possui um Dockerfile próprio:

- `backend/Dockerfile`
- `frontend/Dockerfile`

O front-end é compilado com Node.js e servido com Nginx. O back-end é compilado com o SDK do .NET 8 e executado com a imagem ASP.NET Runtime.

## 7. Docker Compose

O arquivo `docker-compose.yml` organiza os dois serviços:

- `backend` — container `orbitboard-api`;
- `frontend` — container `orbitboard-web`.

Comando principal:

```bash
docker compose up --build
```

Em situações nas quais as imagens já estão construídas localmente, também pode ser utilizado:

```bash
docker compose up --no-build
```

## 8. URLs da solução

| Recurso | URL |
|---|---|
| Front-end | http://localhost:5173 |
| Back-end | http://localhost:5200 |
| Swagger | http://localhost:5200/swagger |
| Health check | http://localhost:5200/health |

## 9. Estrutura resumida

```text
denken-modulo-5-integracao-fullstack/
├── backend/
│   ├── OrbitBoard.Api/
│   └── Dockerfile
├── frontend/
│   ├── src/
│   ├── Dockerfile
│   └── nginx.conf
├── docs/
├── docker-compose.yml
├── .gitignore
└── README.md
```
