# Build stage
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package.json package-lock.json ./

# Install dependencies
#RUN npm install
RUN ./node_modules/.bin/vite build
# Copy source code
COPY . .

# Build React app
RUN npm run build

# Production stage
FROM node:18-alpine

# Install serve to run the built app
RUN npm install -g serve

WORKDIR /app

# Copy built files from builder
COPY --from=builder /app/dist ./dist

# Expose port 3000
EXPOSE 3000

# Serve the React app
CMD ["serve", "-s", "dist", "-l", "8000"]
