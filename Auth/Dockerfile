# Use an official Node.js runtime as a parent image
FROM node:21
LABEL authors="mnmustafa1109"
# Set the working directory
WORKDIR /usr/src/app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Bundle app source
COPY . .

# Expose the port the app runs on
EXPOSE 4235

# Command to run the app
CMD ["npm", "start"]
