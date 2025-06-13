# Use official Node image
FROM node:16 AS build

# Set working directory
WORKDIR /app

# Copy dependencies
COPY package.json yarn.lock ./

# Install dependencies using Yarn 4
RUN yarn install

# Copy rest of app
COPY . .

# Build
RUN yarn build

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Copy built app to Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Copy custom Nginx config (optional)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]