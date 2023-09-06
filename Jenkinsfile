pipeline {
    agent {
        label 'BuildandRelease'
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

        stage("Deploy the Application") {
            steps {
                sh "docker build -t java-web-app1:${env.IMAGE_TAG} ." //Build image
                sh "docker run -d -p 8080:8080 --name BELIEVE java-web-app1:${env.IMAGE_TAG}" //Run container from Image
                //deploy adapters: [tomcat9(credentialsId: 'f72e2a62-f1b1-4816-b85c-42ac10f9fa16', path: '', url: 'http://172.31.95.105:8080')], contextPath: null, war: 'target/BELIEVE.war'
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
