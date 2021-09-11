# React - Dev Setup and Deployment

This assignment is intented to help you set up your development environment for React. You will create a simple React App and deploy using one of the methods covered in lecture.

## Step 1
- Install `npx` following the instructions here: https://www.npmjs.com/package/npx
- run `npx create-react-app my-first-app` to create the React application
- In the newly created app, replace the contents of `App.js` including your name:

```
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <p>Hello CSCI E-39!</p>
        <p>
          My name is ____________
        </p>
      </header>
    </div>
  );
}

export default App;
```

- run `npm install`
- start the app with `npm start`
- verify the app is running

## Step 2
Deploy the application using one of the methods covered in class: Github Pages, Render, or AWS. If you prefer to use a different service, explain your choice and process.

## Submitting
Edit this file (README.md) and complete the following:

- URL to live application: 
- How did you deploy it?
- What code editor are you using?

That is all!


---------------------------------------------------------------
URL: http://74.208.183.29:3001/

I deployed it by copy the files to the server via an SFTP process in the editor.
The application is deployed on one of my test servers.

It is deployed in docker. The reason for my choice is that I need to be able to deploy a React application for a Production-ready environment and Docker or 
Kubernetes is the preferred enterprise environment.

Dockfile:
#pull official base image
FROM node:16.5.0-alpine
WORKDIR /usr/app
COPY package.json .
RUN npm install
RUN mkdir node_modules/.cache && chmod -R 777 node_modules/.cache
COPY . .
CMD ["npm", "run", "start"]

Docker-compose.yml

version: '3.3'

services:

  my-first-app:
    container_name: my-first-app
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - '.:/app'
      - '/app/node_modules'
    ports:
      - 3001:3000
    environment:
      - CHOKIDAR_USEPOLLING=true

After all of the files are uploaded. I run the docker command:

docker-compose  build
docker-compose up -d

The docker image is built and start, and all I have to do is to connect to: 
http://74.208.183.29:3001/

I am using JetBrains WebStorm as my editor.

