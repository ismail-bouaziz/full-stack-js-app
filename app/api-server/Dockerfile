# ---------- BASE ----------
FROM node:20-alpine AS base

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 5050

# ---------- DEV ----------
FROM base AS dev
RUN npm install -g nodemon
CMD ["nodemon", "app"]