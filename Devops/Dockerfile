# Use Node.js as the base image for building
FROM node:20 AS build

# Set the working directory
WORKDIR /app

# Copy the package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the entire project into the container
COPY . .

# Build the React app
RUN npm run build

# Use NGINX as the base image for serving the React app
FROM nginx:1.23

# Set environment variables
ENV NODE_ENV=production

# Remove the default NGINX static content
RUN rm -rf /usr/share/nginx/html/*

# Copy the build output to NGINX's default folder
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start NGINX server
CMD ["nginx", "-g", "daemon off;"]
