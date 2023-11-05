pipeline {
    agent any

    environment {
        MAVEN_HOME = 'C:\Users\salma\Desktop\jenkins\apache-maven-3.9.5'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh '${MAVEN_HOME}/bin/mvn clean package'
                }
            }
        }

        stage('Deployment') {
            steps {
                script {
                    withCredentials([
                        usernamePassword(credentialsId: 'TomcatCreds', usernameVariable: 'tomcat', passwordVariable: 'password')
                    ]) {
                        deploy contextPath: 'mvnPipeline', war: '**/*.war'
                    }
                }
            }
        }
    }
}
