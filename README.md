# Udemy course 
https://knlearning.udemy.com/course/learn-devops-ci-cd-with-jenkins-using-pipelines-and-docker/learn/

## Steps
1 - Run jenkins from a container:
The Jenkins server will be running as a docker container: Make sure if you have docker service running in your local env:
If you are using Windows S.O, you can run a docker from the WSL2.
1.1 - First we need to build the Jenkins image:
Go to the jenkins_master folder:
```commandline
docker build . -t jenkins_course
```
Make sure you are inside the folder that contains the Dockerfile.
Very important detail:
In the Dockerfile line 14 - It is expecting a group number for the docker group:
```dockerfile
# groupadd -g 999 docker && \
```
This group need to be exactly the docker ID number running in your local host. The Jenkins container will connect the docker sock with
your local env socks, like a symbolic link. 
When Jenkins container runs docker service, it will run it from your local env. So, you need to check it docker group is already defined
in your local system.
````commandline
cat /etc/group | grep docker
or
getent group docker
e.g output
docker:x:999:user
````
## Create jenkins_home folder and give permission
mkdir /var/jenkins_home
sudo chown -R 1000:1000 /var/jenkins_home/
Now run the Jenkins image just created with the sock connection parameter:
```commandline
docker run -d -p 8080:8080 -p 50000:50000 -v /var/jenkins_home/:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkins_course
```
Take the installation key from the docker container logs
docker logs -f $container_number
admin admin

## Plugins list
CloudBees Docker Build and Publish plugin on Jenkins
Docker Pipeline
GitHub Branch source
BitBucket Branch source  -- Scan team/project folders

1.2 - Create a new pipeline and set up a Freestyle. 
-- Inform your Git repository where you have your project and docker file do build.
This parameter informs Jenkins where is your project and your docker definitions.
It will build a new image, creating a docker container image and push it to docker hub.
1.3 - Configure the Build as Docker Build and Publish
-- Create a dockerhub repository to save your image into the registry.
Inform build credentials. 
-- Create the gitHub credential, inform user and password.

docker run -p 3000:3000 -d --name my-nodejs-app alexsimple/docker-nodejs-demo

Go to web browser:
http://localhost:3000