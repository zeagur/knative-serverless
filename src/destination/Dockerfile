FROM node:lts-alpine

WORKDIR /app

RUN adduser -S appuser -G root

COPY package*.json ./

RUN npm install

COPY public ./public

COPY .babelrc cities.csv swagger.yaml ./

COPY src ./src

RUN chgrp -R 0 /app
RUN chmod -R g=u /app
USER appuser

EXPOSE 4000

CMD ["npm", "run", "start"]