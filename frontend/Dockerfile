FROM node:22-alpine

WORKDIR /app
COPY vue-practice/ ./
RUN apk update

CMD sh -c "npm ci && npm run dev"
