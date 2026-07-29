Evidências de Testes — OrbitBoard

1. Objetivo

Este documento registra os testes realizados na aplicação OrbitBoard, demonstrando o funcionamento do front-end, do back-end, da API REST, da execução com Docker Compose e das principais operações funcionais do sistema.

2. Ambiente utilizado

Sistema operacional: Windows

Docker Desktop com containers Linux e WSL 2

Back-end: ASP.NET Core .NET 8

Front-end: React com Vite

Servidor web: Nginx

Orquestração: Docker Compose

URLs utilizadas

Front-end: http://localhost:5173

Back-end/API: http://localhost:5200

Swagger: http://localhost:5200/swagger

Health check: http://localhost:5200/health

3. Construção do back-end

Comando

docker build -t orbitboard-backend ./backend

Resultado

A imagem orbitboard-backend:latest foi construída com sucesso e a aplicação iniciou na porta 5200.

Status

Aprovado.

4. Construção do front-end

Comando

docker build -t orbitboard-frontend ./frontend

Resultado

As dependências foram instaladas, o build do React/Vite foi gerado e os arquivos foram servidos pelo Nginx.

Status

Aprovado.

5. Teste do health check da API

Endereço

http://localhost:5200/health

Resultado obtido

{
  "status": "healthy",
  "service": "OrbitBoard.Api"
}

Evidência



Status

Aprovado.

6. Teste do Swagger

Endereço

http://localhost:5200/swagger

Resultado

O Swagger exibiu os endpoints de dashboard, projetos, tarefas, equipe e health check.

Evidência



Status

Aprovado.

7. Teste do front-end

Endereço

http://localhost:5173/dashboard

Resultado

O front-end foi carregado corretamente pelo Nginx.

Status

Aprovado.

8. Integração entre front-end e back-end

Procedimento

O back-end foi iniciado na porta 5200.

O front-end foi iniciado na porta 5173.

O dashboard foi acessado pelo navegador.

O front-end realizou requisições HTTP para a API.

Os dados retornados em JSON foram exibidos na interface.

Resultado obtido

O dashboard exibiu inicialmente:

3 projetos;

5 tarefas;

1 tarefa concluída;

0 tarefas atrasadas;

distribuição de tarefas por status.

Evidência



Status

Aprovado.

9. Execução com Docker Compose

Comando principal previsto

docker compose up --build

Comando utilizado na validação final

docker compose up --no-build

O segundo comando foi utilizado porque as imagens já haviam sido construídas e houve instabilidade temporária de conexão com os registros externos.

Resultado

O Docker Compose criou a rede da aplicação e iniciou:

orbitboard-api
orbitboard-web

Status

Aprovado.

10. Problemas encontrados e correções

10.1 Docker Desktop não iniciado

Problema: o cliente Docker estava instalado, mas o mecanismo Linux não estava disponível.

Correção: o Docker Desktop foi reiniciado e o funcionamento foi confirmado quando docker version passou a exibir as seções Client e Server.

10.2 Bloqueio de CORS

Problema: o front-end publicado inicialmente na porta 8080 não conseguia consumir a API.

Correção: a aplicação foi executada em http://localhost:5173, origem já permitida pela política de CORS da API.

10.3 TLS handshake timeout

Problema: durante alguns builds, o Docker não conseguiu consultar Docker Hub e Microsoft Container Registry.

Correção: após as imagens terem sido construídas, o Compose foi executado com --no-build, utilizando as imagens locais.

10.4 Localização incorreta do docker-compose.yml

Problema: o Compose foi colocado inicialmente dentro da pasta backend.

Correção: o arquivo foi movido para a raiz do projeto, no mesmo nível de backend e frontend.

10.5 Nome das imagens no Compose

Problema: o Compose procurava nomes automáticos diferentes das imagens criadas manualmente.

Correção: foram definidos explicitamente no docker-compose.yml:

orbitboard-backend:latest
orbitboard-frontend:latest

11. Testes funcionais

11.1 Criação de projeto

Procedimento: foi criado o projeto Projeto Teste Docker, com descrição, responsável, status, data inicial e prazo.

Resultado: o projeto foi salvo pela interface e passou a aparecer corretamente na listagem.

Evidência:



Status: Aprovado.

11.2 Edição de projeto

Procedimento: o projeto de teste foi editado para validar a atualização de dados pela API.

Resultado: as informações alteradas foram exibidas corretamente no card do projeto.

Evidência:



Status: Aprovado.

11.3 Criação de tarefa

Procedimento: foi criada a tarefa Validar integração Docker, vinculada ao projeto de teste, com responsável, prioridade, prazo e estimativa.

Resultado: a tarefa foi salva e apareceu corretamente na coluna Backlog.

Evidência:



Status: Aprovado.

11.4 Alteração de status da tarefa

Procedimento: a tarefa foi movimentada pelos seguintes status:

Backlog;

Em andamento;

Em revisão;

Concluída.

Resultado: o card foi transferido corretamente entre as colunas, confirmando a atualização via API.

Evidências:







Status: Aprovado.

11.5 Atualização dos indicadores do dashboard

Procedimento: após a criação do projeto e da tarefa, e após a conclusão da tarefa, o dashboard foi acessado novamente.

Resultado obtido:

Projetos: 4;

Tarefas: 6;

Concluídas: 2;

Atrasadas: 0;

a tarefa Validar integração Docker apareceu na atividade recente como concluída.

Evidência:



Status: Aprovado.

11.6 Exclusão de tarefa

Procedimento: a tarefa Validar integração Docker foi excluída pela interface.

Resultado: a tarefa deixou de aparecer no quadro de tarefas e as contagens voltaram aos valores anteriores.

Evidência:



Status: Aprovado.

11.7 Exclusão de projeto

Procedimento: o projeto de teste foi excluído pela interface.

Resultado: o sistema exibiu a mensagem Projeto excluído. e o projeto deixou de aparecer na listagem.

Evidência:



Status: Aprovado.

12. Conclusão

Os testes realizados confirmaram que a aplicação OrbitBoard possui front-end, back-end e API integrados, com execução em containers Docker e inicialização conjunta por Docker Compose.

A solução apresentou:

comunicação HTTP/JSON entre front-end e API;

documentação dos endpoints por Swagger;

health check da API;

tratamento de estados de carregamento e erro na interface;

criação, edição e exclusão de projetos;

criação, alteração de status e exclusão de tarefas;

atualização automática dos indicadores do dashboard;

execução conjunta dos serviços por Docker Compose.

Todos os testes funcionais previstos foram concluídos com sucesso.