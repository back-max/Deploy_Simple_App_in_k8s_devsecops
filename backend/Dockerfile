FROM node:25-alpine3.21 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install --omit=dev

COPY . .


# no "npm run build" for backend apps
# ---- Stage 2: Run ----
FROM node:25-alpine3.21

RUN addgroup -S appgroup -g 1001 && adduser -S appuser -G appgroup -u 1001

WORKDIR /app

COPY --from=build --chown=appuser:appgroup /app ./app

USER appuser

EXPOSE 5000


CMD ["node", "app/index.js"]