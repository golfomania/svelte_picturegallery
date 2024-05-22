# FROM node:22
FROM node:20.13.0-alpine3.19 AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build && npm prune --production
# ENV PORT 5050
# EXPOSE 5050
# CMD ["node", "build"]

FROM node:20.13.0-alpine3.19
USER node:node
WORKDIR /app
# COPY --from=0 /app/build ./build
COPY --from=builder --chown=node:node /app/build ./build
COPY --from=builder --chown=node:node /app/node_modules ./node_modules
COPY --chown=node:node package.json .
ENV PORT 3000
EXPOSE 3000
CMD ["node", "build"]