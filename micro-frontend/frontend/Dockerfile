# Stage 1: Build the React app
FROM node:14-alpine as build

WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

RUN npm cache clear --force

# Install dependencies
RUN npm install

# Copy the rest of the app's source code to the container
COPY . .

# Build the React app
RUN npm run build

# Stage 2: Serve the React app using a lightweight web server
FROM nginx:alpine

# Copy the build files from the previous stage to the NGINX web server's root directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose the desired port (e.g., 80) for the NGINX server
EXPOSE 80

# Start the NGINX server
CMD ["nginx", "-g", "daemon off;"]
