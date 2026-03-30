# # Build stage
# FROM node:20 AS build

# WORKDIR /app

# # Pass build arguments for environment variables
# ARG VITE_API_URL
# ENV VITE_API_URL=$VITE_API_URL

# COPY package*.json ./
# RUN npm install --legacy-peer-deps

# COPY . .

# RUN npm run build

# # Production stage
# FROM nginx:alpine

# COPY --from=build /app/dist /usr/share/nginx/html

# EXPOSE 80

# CMD ["nginx", "-g", "daemon off;"]

# ###############################
# Step 1: Build stage
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .


# Replace env for docker
# COPY .env.docker .env

# Build React app
RUN npm run build

# Step 2: Serve using nginx
FROM nginx:alpine

# Copy built files
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]