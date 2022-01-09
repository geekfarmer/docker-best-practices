FROM node:12-alpine AS builder
WORKDIR /app
COPY . .
RUN npm ci && npm run build

FROM nginx:1.17
COPY --from=builder /app/build /usr/share/nginx/html