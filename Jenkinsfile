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
        // stage("Deploy the Application") {
        //     steps {
                
        //     }
        // }
    }
}
