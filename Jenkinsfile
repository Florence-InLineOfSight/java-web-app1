pipeline {
    agent {
        label 'java_agent'
    }

    environment {
        IMAGE_TAG = "Default"
    }

    tools {
        maven "maven3.9.4"
    }

    stages {
        stage("Build and Package") {
            steps {
                sh "mvn clean package"      //mvn clean + mvn package
            }
        }

/*
        stage("Static Code Analysis") {     //sonarqube
            steps {
                sh "mvn sonar:sonar"
            }
        }
        stage("Backup to Artifactory") {    //nexus
            steps {
                sh "mvn deploy"
            }
        }
*/

        stage("Deploy in Container") {
            steps {
                sh "docker-compose build"
                sh "docker-compose up -d"
            }
        }

        stage("Backup to DockerHub") {
            steps {
                sh "docker tag java-web-app1:newest florenceomoruyi/java-web-app1:${env.IMAGE_TAG}"
                sh "docker push florenceomoruyi/java-web-app1:${env.IMAGE_TAG}"
            }
        }
    }
}


/*
IMPROVEMENTS (SHORTCOMINGS AND RESOLUTION)
a. Create a variable for image tag (buildnumber) to reduce/remove redundancy
b. Backup images to DockerHub to prevent loss
c. Automatically increase build number in case of frequent builds (webhook trigger)
d. Delete old images and containers

*/
