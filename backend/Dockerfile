# ============== Stage 1: Builder ==============
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install all dependencies (including devDependencies for tests/build)
RUN npm install

# Copy source code
COPY . .

# ============== Stage 2: Production ==============
FROM node:18-alpine

WORKDIR /app

# Copy package files and install only production dependencies
COPY package*.json ./
RUN npm install --omit=dev

# Copy application from builder
COPY --from=builder /app .

# Non-root user (security)
RUN addgroup -g 1001 -S nodejs && adduser -S nodejs -u 1001
USER nodejs

EXPOSE 8080

CMD ["node", "server.js"]
