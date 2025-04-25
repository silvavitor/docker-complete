FROM node

WORKDIR /app

COPY package.json ./

RUN npm install

COPY . .

ENV MONGODB_USERNAME=vitor
ENV MONGODB_PASSWORD=secret

EXPOSE 80

CMD ["npm", "start"]