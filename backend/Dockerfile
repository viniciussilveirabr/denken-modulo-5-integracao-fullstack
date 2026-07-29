# Etapa 1: restaura dependências, compila e publica a API
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copia primeiro os arquivos de solução/projeto para aproveitar o cache do Docker
COPY ["OrbitBoard.Api.sln", "./"]
COPY ["OrbitBoard.Api/OrbitBoard.Api.csproj", "OrbitBoard.Api/"]

RUN dotnet restore "OrbitBoard.Api.sln"

# Copia o restante do código-fonte
COPY . .

WORKDIR "/src/OrbitBoard.Api"
RUN dotnet publish "OrbitBoard.Api.csproj" \
    --configuration Release \
    --output /app/publish \
    /p:UseAppHost=false

# Etapa 2: imagem final, menor, apenas para executar a aplicação
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

ENV ASPNETCORE_URLS=http://+:5200
ENV ASPNETCORE_ENVIRONMENT=Development

EXPOSE 5200

COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "OrbitBoard.Api.dll"]
