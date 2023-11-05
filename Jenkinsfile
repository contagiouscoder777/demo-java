pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    withCredentials([
                        usernamePassword(credentialsId: 'TomcatCreds', usernameVariable: 'tomcat', passwordVariable: 'password')
                    ]) {
                        sh """
                            curl -T target/*.war http://${tomcat}:${password}@localhost:7080/manager/text/deploy?path=/mvnPipeline
                        """
                    }
                }
            }
        }
    }
}

