FROM node:18-alpine
WORKDIR /app/src
COPY ./package.json .
RUN npm install
EXPOSE 8080
COPY . .
CMD [ "node", "index.ts" ]