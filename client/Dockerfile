# Use an official Node runtime as a parent image
FROM node:14

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Build the React app
RUN npm run build

# Serve the React app using a static server
RUN npm install -g serve
#  serve on port 1235
# Set the command to run the app
CMD ["serve", "-s", "build", "-l", "1235"]
