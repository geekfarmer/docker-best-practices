FROM node:12-stretch

USER node

RUN mkdir /home/node/complicated-node-app

WORKDIR /home/node/complicated-node-app

# Layers
# Copy first package and package-lock to add caching layers to build docker image fast if no changes needed in packages
COPY --chown=node:node package.json package-lock.json ./

# Recommend to run npm ci instead of npm install to install specific version of package-lock.json. It is faster also.
RUN npm ci

COPY --chown=node:node . .

EXPOSE 3000

CMD ["node", "index.js"]
