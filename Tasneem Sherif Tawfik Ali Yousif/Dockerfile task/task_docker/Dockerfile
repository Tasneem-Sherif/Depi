FROM node:20 AS builder
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
RUN npm run build
RUN npm prune --omit=dev
FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/package*.json .
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist
RUN apk add --no-cache curl
RUN adduser -D -u 1001 appuser
USER appuser
HEALTHCHECK --interval=5s --timeout=2s --start-period=5s \
  CMD curl -f http://127.0.0.1:4000/health || exit 1
CMD ["node", "dist/index.js"]