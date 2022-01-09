FROM node:12-stretch

# Don't use root user, because with root user access we can do whatever we want.
USER node

# Change work directory
WORKDIR /home/node/node-app

COPY --chown=node:node app.js index.js

CMD ["node", "index.js"]