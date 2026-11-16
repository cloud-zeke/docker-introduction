FROM node:22-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
COPY src ./src 
COPY public ./public
RUN npm ci && npm run build

FROM node:22-alpine AS production
WORKDIR /app
RUN npm install -g serve && addgroup -S appgroup && adduser -S -G appgroup appuser
COPY --from=build /app/build ./build
USER appuser
EXPOSE 3000
CMD [ "serve", "-s", "build" ]