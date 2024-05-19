# Dockerfile for frontend

# Use an official Node.js runtime as a parent image
FROM node:18

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the app
RUN npm run build

# Install a web server
RUN npm install -g serve

# Command to run the app
CMD ["serve", "-s", "build"]

# Expose the port the app runs on
EXPOSE 3006
