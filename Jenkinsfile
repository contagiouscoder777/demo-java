pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deployment') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'TomcatCreds', usernameVariable: 'tomcat', passwordVariable: 'password')
                ]) {
                    bat "curl -u ${tomcat}:${password} -T target/*.war http://your-tomcat-server:7080/manager/text/deploy?path=/mvnpipelines"
                }
            }
        }
    }
}
