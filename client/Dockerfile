# Build stage
FROM node:16.13.2-alpine as build
WORKDIR /1132_frontend
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Nginx stage
FROM nginx:1.21.5-alpine
# Copy the build files to the nginx directory
COPY --from=build /1132_frontend/build /usr/share/nginx/html
# Copy the nginx configuration file
COPY nginx.conf /etc/nginx/nginx.conf
# Expose port 1132
EXPOSE 1132
CMD ["nginx", "-g", "daemon off;"]
