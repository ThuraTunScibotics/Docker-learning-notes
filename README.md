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

Check Node Images version list here; https://hub.docker.com/_/node/tags?page=1
We use the lightest node alpine `current-alpine3.17`, You can search yoursel in tag filters. And then open `vs-code` in the directory where the node have been installed. Create the new file with the file name **`Dockerfile`**, and then write the fillowing in the file.
```
# FROM node:[tag-name]
FROM node:current-alpine3.17
```
Open Terminal;
```
cd react-app

sudo docker build -t react-app .    # build docker image

sudo docker image ls    # list the docker images you have installed
```
Test the installed image;
```
sudo docker run -it react-app

'''
Welcome to Node.js v20.0.0.
Type ".help" for more information.
> const x = 1
undefined
> console.log(x)
1
undefined
> 
(To exit, press Ctrl+C again or Ctrl+D or type .exit)
> 
'''
```
We cannot run the image bash as the light `alpine` image we installed did not come with bash. So we will run with sh(shell).
```
sudo docker run -it react-app sh

'''
/ # ls
bin    etc    lib    mnt    proc   run    srv    tmp    var
dev    home   media  opt    root   sbin   sys    usr
/ # node --version
v20.0.0
/ # 
'''
```

### Copying Files and Directories and rebuild the image
Open VS code, and edit the `Dockerfile` by adding `WORKDIR` and `COPY`.
```
FROM node:current-alpine3.17
WORKDIR /app
COPY . .
```
Open Terminal to rebuild the image;
```
sudo docker build -t react-app .
```
And then, run the sh (shell);
```
sudo docker run -it react-app sh

/app # ls
Dockerfile         node_modules       package.json       src
README.md          package-lock.json  public             yarn.lock
/app # 
```
Now, we can see all the files that include `node_modules`.
