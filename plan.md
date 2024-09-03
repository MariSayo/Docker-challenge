Much of this may be wrong apologies to all who read
- need to update and change stuff.

Commands

git clone <Repo url>
    npx create-next-app@latest .
    npm install
    npm run dev
    check http://localhost:3000 

    install docker desktop and docker vscode plugin
    create docker file  ctrl+Shift+P
    docker build: docker build -t my-nextjs-app .

    docker build -t automate-me-v2-dev -f Dockerfile.dev .

    In the above code the automate-me-v2-dev is the same as the name you gave the file in package.json/ -f unecessary if you leave blank
    Run the Docker Container:

    Run the container with port forwarding:

    docker run -p 3000:3000 my-nextjs-app (the stuff after 3000 is the file name)

            access the application in your browser at http://localhost:3000.

**Step 3: Enable Live Reloading with Docker Volumes**
    Stop and Remove Existing Container:
        Stop and remove the running container:

        docker ps
docker stop <container_id>
docker rm <container_id>


    Run the container, mounting the app directory as a volume:

    docker run -p 3000:3000 -v $(pwd):/usr/src/app my-nextjs-app
    (possibly wrong)
    docker run -p 3000:3000 -v %(pwd)/app:app/app (name of file (automate-me-v2-dev))


**PRODUCTION**

      In the root of your application, create a Dockerfile.prod:- HOW??

        # Use Node.js 18 as the base image
FROM node:18-alpine

# Set environment variable
ENV NODE_ENV=production

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Copy the rest of the application files
COPY . .

# Build the application
RUN npm run build

# Expose the application port
EXPOSE 3000

# Set the default command to run the application
CMD ["npm", "start"]

Kinda meant to look like above may not be exact.

build image:
docker build -t my-nextjs-app-prod -f Dockerfile.prod .

run production container: 
docker run -p 3000:3000 my-nextjs-app-prod

http://localhost:3000 

///////////////////////////////////////////////////////////////

**PLAN BUT SHORTER AND JUST COMMANDS**

# Step 1: Set Up and Verify the Next.js Application

# Clone the empty repository
git clone <repository-url>
cd <repository-folder>

# Create a new Next.js application
npx create-next-app@latest ./

# (Answer the prompts: TypeScript - No, ESLint - Yes, all others - Default)

# Install dependencies and run the development server
npm install
npm run dev

# Verify the application is running at http://localhost:3000


# Step 2: Containerize the Application for Development

# Create a Dockerfile in the root directory of your project with the following content:
# ---------------------------------------------------
# FROM node:18-alpine
# ENV NODE_ENV=development
# WORKDIR /usr/src/app
# COPY package*.json ./
# RUN npm install
# COPY . .
# EXPOSE 3000
# CMD ["npm", "run", "dev"]
# ---------------------------------------------------

# Build the Docker image
docker build -t my-nextjs-app .

# Run the Docker container with port forwarding
docker run -p 3000:3000 my-nextjs-app

# Verify the application is running in Docker at http://localhost:3000


# Step 3: Enable Live Reloading with Docker Volumes

# Stop and remove the running container
docker ps
docker stop <container_id>
docker rm <container_id>

# Run the container with a volume to enable live reloading
docker run -p 3000:3000 -v $(pwd):/usr/src/app my-nextjs-app

# Make changes to the page.js file in VSCode and verify the changes are reflected in the browser


# Step 4: Containerize the Application for Production

# Create a Dockerfile.prod in the root directory of your project with the following content:
# ---------------------------------------------------
# FROM node:18-alpine
# ENV NODE_ENV=production
# WORKDIR /usr/src/app
# COPY package*.json ./
# RUN npm install --only=production
# COPY . .
# RUN npm run build
# EXPOSE 3000
# CMD ["npm", "start"]
# ---------------------------------------------------

# Build the production Docker image
docker build -t my-nextjs-app-prod -f Dockerfile.prod .

# Run the production Docker container
docker run -p 3000:3000 my-nextjs-app-prod

# Verify the application is running in production mode at http://localhost:3000


# Step 5: Clean Up (Optional)

# Stop and remove the running production container
docker ps
docker stop <container_id>
docker rm <container_id>

# Remove the Docker images (if needed)
docker rmi my-nextjs-app
docker rmi my-nextjs-app-prod




