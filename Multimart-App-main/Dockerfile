# Stage 1: Build the React app
FROM node:18 AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app for production
RUN npm run build

# Stage 2: Serve the React app using serve
FROM node:18-alpine

# Install serve globally
RUN npm install -g serve

# Set working directory
WORKDIR /app

# Copy the build output to the second stage
COPY --from=build /app/build .

# Expose port 3000 to the outside world
EXPOSE 3000

# Start the app using serve
CMD ["serve", "-s", ".", "-l", "3000"]

