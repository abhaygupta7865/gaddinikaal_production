# Step 1: Use an official Node.js image to build the app
FROM node:16-alpine AS build

# Step 2: Set working directory in container
WORKDIR /app

# Step 3: Copy package.json and package-lock.json to the container
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the application code
COPY . .

# Step 6: Build the React app for production
RUN npm run build

# Step 7: Use a lightweight web server to serve the built app
FROM nginx:alpine

# Step 8: Copy the built app from the previous stage to the web server's directory
COPY --from=build /app/dist /usr/share/nginx/html

# Step 9: Expose the port the app will run on
EXPOSE 8081

# Step 10: Start the Nginx server
CMD ["nginx", "-g", "daemon off;"]
