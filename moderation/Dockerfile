FROM node:alpine

WORKDIR /app

COPY package*.json ./

RUN npm i

COPY . .

EXPOSE 4003

CMD ["node", "index.js"]

# docker build -t ms-moderation .
