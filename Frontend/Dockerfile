# Stage 1: Build the Angular app
FROM node:17 AS build

WORKDIR /app
COPY . .

RUN npm install
RUN npm run build --prod

# Stage 2: Serve the Angular app with Nginx
FROM nginx:alpine

# Copy custom Nginx config if needed
# COPY nginx.conf /etc/nginx/nginx.conf

# Copy built Angular files to Nginx directory
COPY --from=build /app/dist/catalog /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
