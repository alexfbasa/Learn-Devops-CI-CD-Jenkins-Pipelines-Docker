# Udemy course 
https://knlearning.udemy.com/course/learn-devops-ci-cd-with-jenkins-using-pipelines-and-docker/learn/

docker build . -t jenkins_course

docker run --name jenkins_course -p 8080:8080 -p 50000:50000 --env HTTP_PROXY="http://localhost:8080" --env HTTPS_PROXY="https://localhost:8080" -v /var/jenkins_home:/var/jenkins_home jenkins_course
