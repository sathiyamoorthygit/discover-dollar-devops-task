# Build stage
FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Angular production build
RUN npm run build --prod

# Serve stage
FROM nginx:alpine

WORKDIR /usr/share/nginx/html

# Copy everything from dist folder (whatever name is generated)
COPY --from=build /app/dist/. .

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
