# Step 1: Build the React app
FROM node:18 as build

# Set working directory inside container
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the code
COPY . .

# Build the React app for production
RUN npm run build

# Step 2: Serve the built files using Nginx
FROM nginx:alpine

# Copy build output to nginx's public directory
COPY --from=build /app/build /usr/share/nginx/html

# Copy a custom nginx config if needed (optional)
COPY nginx.conf /etc/nginx/conf.d/default.conf


# Expose port 80
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

