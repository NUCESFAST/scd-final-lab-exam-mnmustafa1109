FROM node:21
LABEL authors="mnmustafa1109"

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 4009

CMD ["node", "index.js"]
