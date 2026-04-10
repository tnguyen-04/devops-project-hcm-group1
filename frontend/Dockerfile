# ============== Stage 1: Builder ==============
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install all dependencies
RUN npm install

# Copy source and build
COPY . .
RUN npm run build

# ============== Stage 2: Production (serve static) ==============
FROM node:18-alpine

WORKDIR /app

# Only need serve to run static build
RUN npm install -g serve

# Copy built assets from builder
COPY --from=builder /app/build ./build

# Non-root user (security)
RUN addgroup -g 1001 -S nodejs && adduser -S nodejs -u 1001
USER nodejs

EXPOSE 3000

CMD ["serve", "-s", "build", "-l", "3000"]
