FROM node:16-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm i

COPY . ./

RUN npm run build

FROM node:16-alpine as production

WORKDIR /app

COPY --from=builder /app/package*.json ./

RUN npm i --omit=dev \
  && npm i -g pm2

COPY --from=builder /app/dist ./dist/

COPY ./ecosystem.config.js ./  

ENTRYPOINT ["pm2-runtime", "start", "ecosystem.config.js"]