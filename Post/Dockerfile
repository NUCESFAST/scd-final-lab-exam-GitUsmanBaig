# Use an official runtime as a parent image
FROM node:20.13.1-alpine3.19

# Set the working directory in the container
WORKDIR /1132_backend

# Copy the current directory contents into the container at /usr/src/app
COPY package*.json ./

# Install any needed packages specified in package.json
RUN npm install

# Copy the rest of the application code
COPY . .

# Make port 8000 available to the world outside this container
EXPOSE 3132

# Define environment variable, the port and MONGO_DB_SECRET
ENV PORT=3132

# Run app.py when the container launches
CMD ["node", ".index.js"]
