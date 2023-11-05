pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

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
                            curl -u ${tomcat}:${password} -T target/*.war http://your-tomcat-server:8080/manager/text/deploy?path=/contextPath
                        """
                    }
                }
            }
        }
    }
}
