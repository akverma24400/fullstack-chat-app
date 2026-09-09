# Stage 1: Install production dependencies
FROM node:22-alpine AS dependencies

WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev


# Stage 2: Run the backend
FROM node:22-alpine AS production

WORKDIR /app

ENV NODE_ENV=production
ENV PORT=5001

COPY --from=dependencies --chown=node:node /app/node_modules ./node_modules
COPY --chown=node:node package*.json ./
COPY --chown=node:node src ./src

USER node

EXPOSE 5001

CMD ["node", "src/index.js"]
