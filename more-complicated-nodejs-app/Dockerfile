
# Node:Alpine is a light weigtht Linux distribution and more secure than Debian. It is based on the Linux kernel and uses the glibc library.
# Best to use with production servers.
# Use to make things even faster, lighter, cheaper and more secure.
# After using node-alpine our node-app image size is reduced to 86MB from 981MB
# 86MB
FROM node:12-alpine
# 981MB
# FROM node:12-stretch

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
