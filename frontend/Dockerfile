
FROM node:18-alpine AS builder

WORKDIR /app
COPY package*.json ./


RUN npm install --legacy-peer-deps

COPY . .

RUN npm run build


FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html

# Optional: Copy a custom Nginx configuration file if needed
COPY nginx/default.conf /etc/nginx/conf.d/default.conf


EXPOSE 80 

# The Nginx image already has a default command to start the server.
 CMD ["nginx", "-g", "daemon off;"]