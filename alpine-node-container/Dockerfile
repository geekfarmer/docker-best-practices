#We're down to 56MB compared to 86MB with the official node:12-alpine container.
FROM alpine:3.10

RUN apk add --update nodejs npm
RUN addgroup -S node && adduser -S node -G node

USER node

RUN mkdir /home/node/complicated-node-app
WORKDIR /home/node/complicated-node-app

# Layers
# Copy first package and package-lock to add caching layers to build docker image fast if no changes needed in packages
COPY --chown=node:node package.json package-lock.json ./
# Recommend to run npm ci instead of npm install to install specific version of package-lock.json. It is faster also.
RUN npm ci

COPY --chown=node:node . .

CMD ["node", "index.js"]
