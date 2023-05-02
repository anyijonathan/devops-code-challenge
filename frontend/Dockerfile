# Use an official Node.js runtime as a parent image
FROM node:14-alpine
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./
RUN npm install
COPY . .
ENV NODE_ENV production
ENV PORT 3000

# Expose the port that the application will run on
EXPOSE $PORT

# Start the application
CMD ["npm", "start"]
