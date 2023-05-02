# Use an official Node.js runtime as a parent image
FROM node:14-alpine
WORKDIR /app
COPY package*.json ./

# Install the dependencies
RUN npm install
COPY . .
ENV NODE_ENV production
ENV PORT 5000

# Expose the port that the application will run on
EXPOSE $PORT

# Start the application
CMD ["npm", "start"]
