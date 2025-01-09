FROM node

WORKDIR /app

COPY package*.json ./

RUN npm i

COPY . .

EXPOSE 4005

CMD ["node", "index.js"]

# docker build -t ms_event_bus .