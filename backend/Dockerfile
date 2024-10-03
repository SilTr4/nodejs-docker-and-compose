FROM node:16-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm сi

COPY . ./

RUN npm run build

FROM node:16-alpine as production

WORKDIR /app

COPY --from=builder /app/package*.json ./

RUN npm сi --omit=dev \
  && npm i -g pm2

COPY --from=builder /app/dist ./dist/

ENTRYPOINT ["pm2-runtime", "start", "ecosystem.config.js"]