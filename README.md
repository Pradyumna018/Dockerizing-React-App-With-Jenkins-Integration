# Rename Your Hostname 
```
sudo hostnamectl set-hostname myapp
/bin/bash
```
# Step-1 : Create EC2 Instance and Install Dependencies
```
sudo apt-get update -y
sudo apt-get install docker.io -y
```
```
sudo usermod -aG docker $USER && newgrp docker
/bin/bash
```
```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
```
```
sudo apt update
sudo apt install fontconfig openjdk-17-jre -y
java -version
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
```
```
docker --version
java -version
```
```
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
# Step-2 : Clone the Repository
```
git clone https://github.com/Pradyumna018/Dockerizing-React-App-With-Jenkins-Integration.git
```
# Step-2 : Create a Dockerfile**

The next step is to create a Dockerfile for our React application. A Dockerfile is a text file that contains instructions for building a Docker image.

In your terminal, navigate to the root directory of your React application and create a new file named `Dockerfile`.

Open the `Dockerfile` in your code editor and add the following contents:

```bash
# Use an official Node runtime as a parent image
FROM node:16

# Set the working directory to /app
WORKDIR /app

# Copy the package.json and package-lock.json to the working directory
COPY ./package*.json ./

# Install the dependencies
RUN npm install

# Copy the remaining application files to the working directory
COPY . .

# Build the application
RUN npm run build

# Expose port 3000 for the application
EXPOSE 3000

# Start the application
CMD [ "npm", "run", "start" ]
```

## Building a Docker Image

Now that we have a Dockerfile for our React application, we can build a Docker image.

Create a new file named `.dockerignore` in the root directory of your React application and add the following line:

```bash
node_modules
```
