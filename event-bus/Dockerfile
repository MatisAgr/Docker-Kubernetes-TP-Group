FROM node:18-alpine

WORKDIR /app

COPY package.json /
RUN npm install

COPY . .

EXPOSE 4005

CMD ["node", "index.js"]

# docker build -t ms_event_bus .