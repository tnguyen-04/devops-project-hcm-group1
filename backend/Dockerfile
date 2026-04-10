# =========================
# Stage 1: Builder
# =========================
FROM node:18-alpine AS builder

WORKDIR /app

# copy package files
COPY package*.json ./

# install ALL dependencies
RUN npm install

# copy source code
COPY . .


# =========================
# Stage 2: Production
# =========================
FROM node:18-alpine

WORKDIR /app

# copy package files only
COPY --from=builder /app/package*.json ./

# install production dependencies only
RUN npm install --only=production

# copy app source
COPY --from=builder /app .

# expose backend port
EXPOSE 8080

# start app
CMD ["node", "server.js"]