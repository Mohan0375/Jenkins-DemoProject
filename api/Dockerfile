# Base image
FROM node:20-alpine

# Working directory inside the container
WORKDIR /app

# Copy package files first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the project
COPY . .

# Backend listens on port 5000
EXPOSE 5000

# Start the application
CMD ["npm", "start"]
