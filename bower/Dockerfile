FROM node:alpine

RUN apk add --no-cache git && npm install --global bower
WORKDIR /app/
ENTRYPOINT ["bower", "--allow-root"]
