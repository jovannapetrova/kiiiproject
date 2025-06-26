FROM node:18-buster AS nebula-frontend-base

WORKDIR /var/nebula-frontend

COPY ../../package*.json ./

RUN npm install --legacy-peer-deps

COPY . .

EXPOSE 3000

CMD ["npm", "run", "build:start:stage"]
