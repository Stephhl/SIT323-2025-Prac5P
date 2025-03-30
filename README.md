# Dockering a Web Application

## Basic Overview
This project involves containerising a calculator web application that is run from a built image using docker.

## Steps/Instructions
1. Install [Docker](https://www.docker.com/get-started/) and ensure you choose the correct OS for your machine.
    - Check if it's installed by using "docker --version"

2. Create a Dockerfile with the following below:
```bash
FROM node:22

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ENV PORT=3040

EXPOSE 3040

CMD ["npm", "start"]
```

3. Create a .dockerignore to omit all the node modules file
```bash
node_modules
```

4. Create a docker-compose.yml file with the following lines:
```bash
version: "3"
services:
  web:
    image: calcapp
    build: .
    ports:
      - 3040:3040
    environment:
      - NODE_ENV=production
```

5. Build the image through using the command "docker build -t calcapp ."
    - You can see if the image is built using "docker images"

6. Now, build the image into a container by typing in the terminal "docker run -p (Image ID #)
    - Use "docker ps" to see if container is running
   
7. Check if it is all working correctly by going to a browser and go to <http://localhost:3040/divide?n1=10&n2=1>
   
8. Congratulations! You have containerised a simple calculator web application.
