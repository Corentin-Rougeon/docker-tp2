FROM node:12-alpine3.9

WORKDIR /usr/share/app/

COPY package.json .

RUN npm install

COPY . .

CMD ["node", "src/index.js"]