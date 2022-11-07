FROM node:18-alpine
WORKDIR /app/src
COPY ["./packages/server/package.json","./"]
RUN npm install
EXPOSE 8082
COPY . .
CMD [ "node", "index.ts" ]