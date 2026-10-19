
# Stage 1: Build the React application
FROM node:22-bookworm-slim AS build

WORKDIR /app

# Pass the backend API URL during the Docker build
ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}

# Install dependencies
COPY package*.json ./
RUN npm ci

# Copy source code and build the production application
COPY . .
RUN npm run build

# Stage 2: Serve the production build using Nginx
FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

