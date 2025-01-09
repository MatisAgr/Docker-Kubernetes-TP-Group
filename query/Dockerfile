FROM node:alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm i

COPY . .

EXPOSE 4002

CMD ["node", "index.js"]

# docker build -t ms-query .