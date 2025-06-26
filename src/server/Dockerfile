FROM node:16-alpine AS quantum-backend-base

WORKDIR /srv/quantum-backend

COPY ../../package*.json ./

RUN npm install --legacy-peer-deps

COPY . .

EXPOSE 5000

CMD ["node", "index.js"]