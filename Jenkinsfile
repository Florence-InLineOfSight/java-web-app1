pipeline {
    agent {
        label 'BuildandRelease'
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
        stage("Deploy the Application") {
            steps {
                sh "docker build -t java-web-app1:1.0 ." //Build image
                sh "docker run -d -p 8080:8080 --name BELIEVE java-web-app1:1.0" //Run container from Image
                //deploy adapters: [tomcat9(credentialsId: 'f72e2a62-f1b1-4816-b85c-42ac10f9fa16', path: '', url: 'http://172.31.95.105:8080')], contextPath: null, war: 'target/BELIEVE.war'
            }
        }
    }
}

/*
1. Create our BuildAndRelease agent
2. Configure maven installation
3. maven-sonarqube integration on BuildAndRelease agent
4. maven-nexus integration on BuildAndRelease agent
5. Tomcat configuration

Access application on tomcatserver
*/
