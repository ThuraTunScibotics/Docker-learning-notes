# Docker-learning-notes

### Building Image
Image contains all the files and configuration setting needed to run application;
* A cut-down OS
* Third-part libraries
* Application files
* Environment variables

One we've an Image we can start a Container. A Container is like a kind of virtual machine, and it provides an isolated environment to execute applications. It can be stopped & restarted. It is also a special kind of process like OS, because it has own file system which is provided by the image.

**Pracal with Sample WebApplication**
```
cd react-app

code .    # Open VS code

### !Check the Dependencies! ###

# Install Node
npm install     # npm going to install all 3rd party libraries in react-app project

### !node_modules is added with installed dependencies to the directory after npm install! ###

# Start the project 
npm start
```

Recap Steps to run the project;
1 - Install node & 3rd party dependencies using `npm install`
2 - Start the prject using `npm start`

### Choosing the right base image

Check Node Images version list here; 
We use the lightest node alpine `20.0.0-alpine3.17`, You can search yoursel in tag filters.
```
sudo docker build -t react-app .

sudo docker image ls
```
