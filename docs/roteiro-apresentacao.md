# Roteiro de Apresentação — OrbitBoard

## Duração sugerida

Entre 8 e 12 minutos.

## 1. Abertura — 30 segundos

- Apresentar o nome OrbitBoard.
- Informar os integrantes da equipe.
- Explicar que o projeto foi utilizado para demonstrar integração full stack.

## 2. Finalidade da aplicação — 45 segundos

O OrbitBoard é uma aplicação didática para gerenciamento de projetos, tarefas e equipe. O sistema possui dashboard com indicadores, cadastro de projetos, organização de tarefas e visualização dos integrantes.

## 3. Arquitetura — 1 minuto

Explicar:

- React/Vite no front-end;
- ASP.NET Core .NET 8 no back-end;
- comunicação HTTP com JSON;
- dados mantidos em memória;
- Nginx servindo o front-end;
- Docker Compose iniciando os dois serviços.

## 4. Demonstração da aplicação — 2 minutos

Mostrar:

1. dashboard;
2. tela de projetos;
3. tela de tarefas;
4. tela de equipe;
5. criação ou edição de um registro;
6. atualização do dashboard.

## 5. Demonstração da API — 1 minuto

Abrir o Swagger e mostrar:

- `/health`;
- `/api/dashboard`;
- endpoints de projetos;
- endpoints de tarefas;
- retorno em JSON.

## 6. Docker e ambiente — 1 minuto

Mostrar:

- Dockerfile do back-end;
- Dockerfile do front-end;
- `docker-compose.yml`;
- portas 5173 e 5200;
- comando `docker compose up --build`;
- containers executando.

## 7. Testes e evidências — 1 minuto

Mostrar o arquivo `docs/evidencias-testes.md` e explicar:

- health check aprovado;
- Swagger aprovado;
- front-end aprovado;
- integração aprovada;
- testes de CRUD;
- logs e prints.

## 8. Ajustes realizados — 1 minuto

Explicar:

- criação dos Dockerfiles;
- configuração do Nginx;
- criação do Docker Compose;
- configuração das portas;
- organização da documentação;
- tratamento da origem permitida pelo CORS.

## 9. Dificuldades — 1 minuto

Relatar:

- Docker Desktop inicialmente sem o mecanismo Linux;
- bloqueio de CORS ao usar porta diferente;
- falhas temporárias de TLS nos registros de imagens;
- correção da localização do Compose;
- ajuste dos nomes das imagens.

## 10. Contribuições — 30 segundos

Cada integrante deve explicar brevemente sua participação, por exemplo:

- configuração do back-end e Docker;
- configuração do front-end e Nginx;
- testes e evidências;
- documentação e apresentação.

## 11. Encerramento — 15 segundos

Concluir informando que a equipe conseguiu executar, integrar, testar, documentar e conteinerizar a aplicação full stack.

## Perguntas que a equipe deve saber responder

- Qual é o papel do front-end?
- Qual é o papel do back-end?
- Como os dados trafegam entre as aplicações?
- O que é CORS?
- Para que serve o Dockerfile?
- Para que serve o Docker Compose?
- Qual a diferença entre as portas 5173 e 5200?
- Onde os dados são armazenados?
- Como os erros são tratados?
- Como comprovar que a API está saudável?
