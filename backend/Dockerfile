FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY ["OrbitBoard.Api/OrbitBoard.Api.csproj", "OrbitBoard.Api/"]
RUN dotnet restore "OrbitBoard.Api/OrbitBoard.Api.csproj"

COPY . .
WORKDIR /src/OrbitBoard.Api
RUN dotnet publish "OrbitBoard.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

ENV ASPNETCORE_URLS=http://+:5200
EXPOSE 5200

COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "OrbitBoard.Api.dll"]
