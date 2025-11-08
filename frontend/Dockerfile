FROM node:20.19.5-alpine3.22 AS builder



WORKDIR /app


# Copy all packages
COPY  . .

ENV NODE_OPTIONS=--openssl-legacy-provider


# Install all workspace dependencies from root
RUN npm install 


RUN npm run build  

# Production stage
FROM nginxinc/nginx-unprivileged:alpine3.22-slim

# Copy the built frontend from builder stage
COPY --from=builder /app/build /usr/share/nginx/html

# Create nginx config for SPA routing
COPY nginx.conf /etc/nginx/conf.d/default.conf


EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]





