OrbitBoard — Integração Full Stack

Aplicação didática para gerenciamento de projetos, tarefas e integrantes de equipe, utilizada no Trabalho Final do Módulo 5 — Integração Full Stack da capacitação da CyberLabs.

O objetivo do projeto é demonstrar, de forma prática, a integração entre front-end, back-end/API e infraestrutura conteinerizada, incluindo consumo HTTP/JSON, documentação de endpoints, tratamento de erros, execução com Docker e registro de testes.

Integrantes da equipe

Substitua os campos abaixo pelos nomes reais antes da entrega.

Integrante 1: [Nome completo]

Integrante 2: [Nome completo]

Integrante 3: [Nome completo]

Integrante 4: [Nome completo]

Funcionalidades

A aplicação permite:

visualizar indicadores gerais no dashboard;

listar, criar, editar e excluir projetos;

listar, criar, editar e excluir tarefas;

alterar o status das tarefas entre Backlog, Em andamento, Em revisão e Concluída;

visualizar integrantes da equipe;

consultar os endpoints pelo Swagger;

verificar a disponibilidade da API pelo health check;

executar front-end e back-end em containers Docker.

Arquitetura

A solução está dividida em duas aplicações principais:

Navegador
   |
   | HTTP/JSON
   v
Front-end React + Vite
   |
   | Requisições REST
   v
Back-end ASP.NET Core Web API
   |
   v
Dados mantidos em memória

Front-end

Responsável pela interface, formulários, dashboard, navegação, feedback de carregamento, sucesso e erro e consumo da API REST.

Back-end

Responsável pelos endpoints REST, validações, regras da aplicação, tratamento global de erros, CORS, Swagger e health check.

Dados

A aplicação-base utiliza dados em memória. Portanto, os dados criados durante os testes são reiniciados quando o container do back-end é recriado.

Infraestrutura

Dockerfile próprio para o back-end;

Dockerfile próprio para o front-end;

Nginx para servir o build do React;

Docker Compose para iniciar os dois serviços.

Mais detalhes estão disponíveis em docs/arquitetura.md.

Tecnologias utilizadas

Front-end

React

Vite

JavaScript

HTML5

CSS3

Nginx

Back-end

ASP.NET Core

.NET 8

C#

Swagger / OpenAPI

Infraestrutura e ferramentas

Docker

Docker Compose

Git

GitHub

Visual Studio Code

WSL 2

Estrutura do repositório

denken-modulo-5-integracao-fullstack/
├── backend/
│   ├── OrbitBoard.Api/
│   ├── Dockerfile
│   ├── OrbitBoard.Api.sln
│   └── README.md
├── frontend/
│   ├── src/
│   ├── Dockerfile
│   ├── nginx.conf
│   ├── package.json
│   └── README.md
├── docs/
│   ├── imagens/
│   ├── arquitetura.md
│   ├── contrato-api.md
│   ├── evidencias-testes.md
│   └── roteiro-apresentacao.md
├── docker-compose.yml
├── .gitignore
└── README.md

Pré-requisitos

Para executar a aplicação, é necessário ter instalado:

Docker Desktop;

suporte a containers Linux;

WSL 2 no Windows;

Git, caso o projeto seja clonado pelo GitHub.

Para execução sem Docker, também são necessários:

.NET SDK 8;

Node.js 20 ou superior;

npm.

Execução com Docker Compose

Na raiz do projeto, execute:

docker compose up --build

Caso as imagens já tenham sido construídas e exista instabilidade temporária nos registros externos, execute:

docker compose up --no-build

Para iniciar em segundo plano:

docker compose up -d --no-build

Para visualizar o estado dos serviços:

docker compose ps

Para acompanhar os logs:

docker compose logs -f

Para encerrar e remover os containers e a rede:

docker compose down

URLs de acesso

Com os serviços em execução:

Serviço

URL

Front-end

http://localhost:5173

Dashboard

http://localhost:5173/dashboard

Back-end/API

http://localhost:5200

Swagger

http://localhost:5200/swagger

Health check

http://localhost:5200/health

Execução local sem Docker

Back-end

Acesse a pasta do projeto da API:

cd backend/OrbitBoard.Api

Restaure e execute:

dotnet restore
dotnet run

A API ficará disponível na porta configurada pelo projeto.

Front-end

Em outro terminal:

cd frontend
npm install
npm run dev

O Vite iniciará o front-end, normalmente em:

http://localhost:5173

A variável VITE_API_URL deve apontar para o endereço da API.

Variáveis de ambiente

Front-end

Arquivo de exemplo:

frontend/.env.example

Variável utilizada:

VITE_API_URL=http://localhost:5200

Back-end

No container, são utilizadas:

ASPNETCORE_ENVIRONMENT=Development
ASPNETCORE_URLS=http://+:5200

Principais endpoints

Dashboard

Método

Endpoint

Descrição

GET

/api/dashboard

Retorna os indicadores gerais

Projetos

Método

Endpoint

Descrição

GET

/api/projects

Lista os projetos

GET

/api/projects/{id}

Consulta um projeto

POST

/api/projects

Cria um projeto

PUT

/api/projects/{id}

Atualiza um projeto

DELETE

/api/projects/{id}

Exclui um projeto

Tarefas

Método

Endpoint

Descrição

GET

/api/tasks

Lista e filtra tarefas

GET

/api/tasks/{id}

Consulta uma tarefa

POST

/api/tasks

Cria uma tarefa

PUT

/api/tasks/{id}

Atualiza uma tarefa

PATCH

/api/tasks/{id}/status

Altera o status

DELETE

/api/tasks/{id}

Exclui uma tarefa

Equipe

Método

Endpoint

Descrição

GET

/api/team-members

Lista os integrantes

Saúde da aplicação

Método

Endpoint

Descrição

GET

/health

Verifica se a API está disponível

A documentação completa está disponível no Swagger e em docs/contrato-api.md.

Testes realizados

Foram executados testes manuais de:

build da imagem Docker do back-end;

build da imagem Docker do front-end;

inicialização conjunta com Docker Compose;

health check da API;

abertura do Swagger;

carregamento do front-end pelo Nginx;

integração HTTP/JSON entre front-end e API;

criação, edição e exclusão de projetos;

criação e exclusão de tarefas;

alteração de status de tarefas;

atualização dos indicadores do dashboard;

tratamento de erro quando a API não estava acessível.

Os resultados e prints estão documentados em:

docs/evidencias-testes.md

Problemas encontrados e soluções

Durante a preparação do projeto foram identificados e tratados:

Docker Desktop iniciado sem o mecanismo Linux;

bloqueio de CORS causado por diferença entre as portas do front-end;

instabilidade de rede com erro TLS handshake timeout;

docker-compose.yml posicionado inicialmente na pasta incorreta;

nomes automáticos de imagens diferentes das imagens construídas manualmente.

As correções estão descritas detalhadamente em docs/evidencias-testes.md.

Documentação complementar

Arquitetura da aplicação

Contrato da API

Evidências de testes

Roteiro da apresentação

Contribuição da equipe

Atualize esta seção antes da entrega final.

Integrante

Contribuição

[Nome do integrante 1]

Docker, integração e testes

[Nome do integrante 2]

Front-end e evidências

[Nome do integrante 3]

Back-end e Swagger

[Nome do integrante 4]

Documentação e apresentação

Comandos úteis

# Construir e iniciar todos os serviços
docker compose up --build

# Iniciar utilizando imagens locais
docker compose up --no-build

# Iniciar em segundo plano
docker compose up -d --no-build

# Ver containers
docker compose ps

# Ver logs
docker compose logs -f

# Encerrar os serviços
docker compose down

Observação sobre persistência

O projeto utiliza dados em memória. Ao recriar ou reiniciar o container do back-end, os dados adicionados durante os testes podem retornar ao estado inicial da aplicação.

Status do trabalho

Back-end/API funcionando

Front-end consumindo a API

Swagger disponível

Health check disponível

Dockerfile do back-end

Dockerfile do front-end

Docker Compose

Testes funcionais

Evidências documentadas

Documentação técnica

Integrantes e contribuições revisados

Pipeline CI/CD