If the syntax highlighting doesn't appear to be working on GitHub in your README.md file, it's important to ensure the syntax is correctly defined. GitHub's markdown renderer uses language identifiers after the triple backticks (```), but sometimes it's necessary to ensure you follow the correct pattern for each block.

Here is the correctly formatted version of your README.md with the correct syntax highlighting that should work on GitHub:

Correct Syntax for GitHub Markdown

# React Todo App Docker & Kubernetes Setup

This document outlines the steps to build, push, and deploy the **React Todo App** using Docker and Kubernetes.

## Dockerfile

The Dockerfile used for building the Docker image for the React Todo App:

```dockerfile

# Use a Node.js image as the base
FROM node:16

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json for npm install
COPY package*.json ./

# Install dependencies (npm will be installed by default in the base node image)
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application (if you have a build step)
RUN npm run build

# Expose the port the app runs on
EXPOSE 3000

# Start the application
CMD ["npm", "start"]


############################################################################################################################################################
Docker Commands
1. Build the Docker Image
docker build -t mateenshaikh00/react-todo-app:latest .


2. Push the Docker Image to Docker Hub
docker push mateenshaikh00/react-todo-app:latest

###############################################################################################################################################################

Kubernetes (MicroK8s) Commands
1. Apply the Kubernetes YAML Configuration
microk8s kubectl apply -f my_app.yaml
########################################################################################################################################################


#################################################################################################################################################################
Kubernetes YAML Configuration (my_app.yaml)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: react-todo-app
  labels:
    app: react-todo-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: react-todo-app
  template:
    metadata:
      labels:
        app: react-todo-app
    spec:
      containers:
      - name: react-todo-app
        image: mateenshaikh00/react-todo-app:latest
        ports:
        - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: react-todo-app-service
spec:
  selector:
    app: react-todo-app
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 30964
  type: NodePort

##################################################################################################################################################################
A Deployment with 1 replica running the React Todo app container.
A Service of type NodePort exposing port 3000, making the app accessible from outside the cluster.
Accessing the Application
After applying the Kubernetes configuration, the React Todo App will be running in your Kubernetes cluster. To access the application, you can use the node's IP and the nodePort defined in the Service (30964 in this case).


http://<Node-IP>:30964

![React Todo List](https://raw.githubusercontent.com/mateenshaik/React-Todo-list/main/React-app.png)











