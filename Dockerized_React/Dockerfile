# ---------- Stage 1: Build the React app ----------
FROM node:18-alpine AS build

WORKDIR /app

# Copy package files and install dependencies
COPY my-react-app/package*.json ./
RUN npm install

# Copy source code and build
COPY my-react-app ./
RUN npm run build

# ---------- Stage 2: Serve using Nginx ----------
FROM nginx:alpine

# Copy build output from the first stage
COPY --from=build /app/build /usr/share/nginx/html

# Optional: custom Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
