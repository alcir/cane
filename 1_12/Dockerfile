FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Install curl and build essentials
RUN apt-get update && apt-get install -y \
    curl \
    build-essential

# Install Node.js LTS 16.x as specified in the README
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash - \
    && apt-get install -y nodejs

# Set working directory
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy application source code
COPY . .

# Build static files for production mode
RUN npm run build

# Install the static server globally
RUN npm install -g serve

# Expose port 5001
EXPOSE 5001

# Serve the build folder using the exact flag sequence from the project README
CMD ["serve", "-s", "-l", "5001", "build"]
