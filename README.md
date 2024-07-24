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
# Step-3 : Create Public and Private key
```
ssh-keygen
```
```
cd ~/.ssh
```
Attach your Public key to Github and Private key to Jenkins.

# Step-4 : LogIn inito jenkins
* Install one plugin `Github Integration`
* Create `FreestyleProject`
* Add github repo address in SCM
* Select your branch (master or main)
* Click on Checkbox `GitHub hook trigger for GITScm polling`
* Build Steps -> Excute shell
* Paste this to create and run the container
```
docker build -t react-app:latest .
docker run -d -p 3000:3000 react-app:latest
```
* Save and Apply
# Step-5 : LogIn inito jenkins

You need to configure the webhook on your GitHub repository. Then, on every commit push, Jenkins will be notified.

So, open your repository in the browser, then go to Settings > Webhooks and add a new one.
Then, enter the URL of your Jenkins instance followed by /github-webhook and select the other options depending on your needs.

`GitHub repo -> Settings -> Webhooks -> push type webhook with URL: http(s)://host:<port>/github-webhook/`

# Step-6 : Build your Pipeline

You will get an error `permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post.`

To avoid this error give permission to that file
```
sudo chmod 777 /var/run/docker.sock
```
# Step-7 : Final deployment with Jenkins CICD
Now do some changes in your code and commit it.

It will automatically trigger the pipeleine and your React app will be deployed.

## Thank You❤️
![Screenshot 2024-07-24 233839](https://github.com/user-attachments/assets/900264f2-e877-4588-a969-a3edc53166ac)

