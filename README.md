This is a basic Java Project to deploy a web app using JENKINS, DOCKER...

PROCEDURE
1. Create our BuildAndRelease agent
2. Configure maven installation
3. maven-sonarqube integration on BuildAndRelease agent
4. maven-nexus integration on BuildAndRelease agent
5. Tomcat configuration to access application on tomcatserver

**TO DEPLOY APPLICATION AS A CONTAINER USING DOCKER**
1. Install and configure Docker
2. Create a Dockerfile for building the image
3. Create a stage which:
    - Build the image
    - Run container from image

IMPROVEMENTS (SHORTCOMINGS AND RESOLUTION)
a. Create a variable for image tag (buildnumber) to reduce/remove redundancy
b. Backup images to DockerHub to prevent loss
c. Automatically increase build number in case of frequent builds (webhook trigger)
d. Delete old images and containers
