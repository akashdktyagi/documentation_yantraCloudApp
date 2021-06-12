# Docker Commands:

1. Get all docker images: docker images -a
2. Delete all docker images: docker rmi $(docker images -a -q)
3. List all containers: docker ps -a
4. Stop all containers: docker stop $(docker ps -a -q)
5. Delete all containers: docker rm $(docker ps -a -q)
6. Build simple Docker image: docker build .

7. Build with tags and no cache: docker build --no-cache  -t 333743/java-brains-spring-app-test-v2 .
docker build --no-cache  -t registry.gitlab.com/gk-platform-1/gk-front-end:latest . 
 
8. To run with ports, app will be available on port 80 to outside world
    1. : docker run -p80:8081 333743/java-brains-spring-app-test-v2
    2.      “docker run -d -p 80:80 <image id> “
9. Login to Docker hub using CLI:
    1. Only in case if login does not happen form the CLI: sudo apt install gnupg2 pass
    2. Docker login 
10. Tag the image if not tagged so far:
    1. docker tag 4493b749ba70 333734/java-brains-spring-app-test-v2:v2
11. TO get all the images:
    1. Docker images
12. To push image after login: 
    1. docker push 333734/java-brains-spring-app-test-v2:v2
13. To pull the docker image and run on EC2 instance.
    1. To pull only: docker pull rocker/verse
    2. To pull and run: docker run --rm -p 8787:8787 rocker/verse
14. 

Other Docker commands used to build: use m to detch using —detach-keys; it can be any key
docker run --detach-keys m -it -p 4200:4200 --name angular_app_travel_api gofnussiss/travel-plan-ui:latest
docker pull gofnusiss/travel-plan-api:20200914-142641.b848c1c

*********Login to contaner in linux machine*****
docker exec -it 0f4be028ba4842a12fad4e097f59bde145cd6dc7364f193c0ebddcaa36644e2f /bin/sh; exit


docker-compose down -v

Docker file which worked:
# Base Alpine Linux based image with OpenJDK JRE only
FROM openjdk:8-jre-alpine
WORKDIR /usr/app
EXPOSE 8081
COPY target/JavaBrainsSpringApp-1.0-SNAPSHOT.jar /usr/app
ENTRYPOINT ["sh","-c"]
CMD ["exec java -jar JavaBrainsSpringApp-1.0-SNAPSHOT.jar"]

https://stackify.com/docker-build-a-beginners-guide-to-building-docker-images/

*************************************************************************
Other Sample Docker File
*********************************************************************
FROM alpine/git as clone (1)
WORKDIR /app
RUN git clone https://github.com/spring-projects/spring-petclinic.git

FROM maven:3.5-jdk-8-alpine as build (2)
WORKDIR /app
COPY --from=clone /app/spring-petclinic /app (3)
RUN mvn install

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=build /app/target/spring-petclinic-1.5.1.jar /app
CMD ["java -jar spring-petclinic-1.5.1.jar"]


Docker 

Use below commands and plugins to publish the images in docker registry with tagging from git commit.
https://dzone.com/articles/maven-git-commit-id-plugin
https://phauer.com/2016/version-numbers-continuous-delivery-maven-docker/


All about Docker environment and Arguments passing
https://vsupalov.com/docker-env-vars/#:~:text=If%20the%20Dockerfile%20has%20ARG,can%20start%20containers%20from%20it.

docker pull gofnusiss/travel-plan-ui:5f01d7238baa8050feac1070351f8744225cf2f8

docker run  -p 4200:4200 gofnusiss/travel-plan-ui:5f01d7238baa8050feac1070351f8744225cf2f8

# Docker Compose:

Cheat Sheet links:

https://devhints.io/docker-compose

docker-compose start. => only to start containers which were previously created already
docker-compose stop
docker-compose pause
docker-compose unpause
docker-compose ps
docker-compose up. ==> to start all the containers afresh mentioned in the compose file.
docker-compose down



//*******************************
Install docker compose on Debian 10 i.e. bitnami Jenkins: 
https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-debian-10
These are the commands mentioned in the link:

sudo curl -L https://github.com/docker/compose/releases/download/1.25.3/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

docker-compose  -f ./microservicecloud/docker-compose.yml up —build


//*************PARAMATRIZE Docker compose file
1. Create .env file and add a dummy value to the variable
2. like: tag_name=123
3. Then pre-append the name of the tag and its value infront of the docker-compose file:
4. example: sudo api_tag=$tag docker-compose -f microservicecloud/docker-compose.yml up -d


