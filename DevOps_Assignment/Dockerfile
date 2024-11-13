# Use a Node.js image as the base
FROM node:16

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json for npm install
COPY package*.json ./

# Install dependencies (npm will be installed by default in the base node image)
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application (if you have a build step)
RUN npm run build

# Expose the port the app runs on
EXPOSE 3000

# Start the application
CMD ["npm", "start"]