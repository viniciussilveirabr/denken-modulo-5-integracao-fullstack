# Etapa 1: instala as dependências e gera o build do React/Vite
FROM node:20-alpine AS build
WORKDIR /app

# Copia primeiro os arquivos de dependências para aproveitar o cache do Docker
COPY package.json package-lock.json ./
RUN npm ci

# Copia o restante do projeto
COPY . .

# URL pública da API usada pelo navegador
ARG VITE_API_URL=http://localhost:5200
ENV VITE_API_URL=${VITE_API_URL}

RUN npm run build

# Etapa 2: serve os arquivos estáticos com Nginx
FROM nginx:1.27-alpine AS runtime

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -qO- http://localhost/health || exit 1

CMD ["nginx", "-g", "daemon off;"]
