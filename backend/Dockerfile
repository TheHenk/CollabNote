# --- Build stage ---
FROM node:20 AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# --- Runtime stage ---
FROM node:20-slim
WORKDIR /app
ENV NODE_ENV=production
COPY package*.json ./
RUN npm ci --omit=dev
COPY --from=build /app/dist ./dist

# IMPORTANT: tell the app & proxy which port to use
ENV PORT=4000
EXPOSE 4000

CMD ["node", "dist/main.js"]
