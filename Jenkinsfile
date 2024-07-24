pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
           
        // stage('Verify Sonar') {
        //     steps {
        //         sh "mvn clean verify sonar:sonar -Dsonar.projectKey=aastha -Dsonar.projectName='aastha' -Dsonar.host.url=http://192.168.1.72:9000 -Dsonar.token=sqp_f1d871675a8e7f8e046a7c5c77738c90c62e760c"
        //     }
        // }

        stage('Build') {
            steps {
                sh "mvn clean install -Dmaven.test.skip=true"
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war'
            }
        }

        stage('deployment') {
            steps {
                deploy adapters: [tomcat9(url: 'http://192.168.1.49:8082/', 
                    credentialsId: 'tomcatCreds')], 
                    war: 'target/*.war', 
                    contextPath: 'aastha1'
            }
        }

    }
}
