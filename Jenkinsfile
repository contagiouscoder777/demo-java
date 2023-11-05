pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' // Assuming 'MAVEN_HOME' is the name of the Maven tool in your Jenkins configuration
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
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
