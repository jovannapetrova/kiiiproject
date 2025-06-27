# Фаза 1: Build фаза
FROM node:18-buster AS builder
WORKDIR /app
# Копирај package files прво за подобро кеширање
COPY package*.json ./
RUN npm install --legacy-peer-deps
# Копирај го остатокот од кодот
COPY . .
# Изгради ја апликацијата
RUN npm run build

# Фаза 2: Production фаза
FROM node:18-buster-slim AS production
WORKDIR /var/nebula-frontend
# Копирај само потребните production dependencies
COPY package*.json ./
RUN npm ci --only=production --legacy-peer-deps && npm cache clean --force
# Копирај ги само built files од builder фазата
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/public ./public
# Копирај други потребни конфигурации (ако има)
COPY --from=builder /app/next.config.js ./
COPY --from=builder /app/.env* ./

EXPOSE 3000
# Користи production start command
CMD ["npm", "start"]