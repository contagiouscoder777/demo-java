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
                mvn clean package
            }
        }

        stage('Deploy') {
            steps {
                // Deploy war/ear to Tomcat server
                withCredentials([
                    usernamePassword(credentialsId: 'TomcatCreds', usernameVariable: 'tomcat', passwordVariable: 'password')
                ]) {
                    sh """
                        cp target/*.war ${TOMCAT_HOME}/webapps/
                        sh ${TOMCAT_HOME}/bin/startup.sh
                    """
                }
            }
        }
    }
}
