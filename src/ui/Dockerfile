FROM node:lts-alpine AS ui

WORKDIR /app

RUN adduser -S appuser -G root

COPY client/package.json client/package-lock.json ./

RUN npm install

COPY client/. ./

RUN chgrp -R 0 /app
RUN chmod -R g=u /app
USER appuser

ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm run build

FROM node:lts-alpine AS release

WORKDIR /app

RUN adduser -S appuser -G root

COPY --from=ui /app/build client/build

COPY package*.json ./

RUN npm install

COPY index.js ./

RUN chgrp -R 0 /app
RUN chmod -R g=u /app
USER appuser

EXPOSE 3000

CMD ["node", "index.js"]
