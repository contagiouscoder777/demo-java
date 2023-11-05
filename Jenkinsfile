pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {
        stage('Build') {
    steps {
        script {
            bat 'mvn clean package'
            dir('target') {
                bat 'dir'
            }
        }
    }
}


        stage('Deployment') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'TomcatCreds', usernameVariable: 'tomcat', passwordVariable: 'password')
                ]) {
                    bat "curl -u ${tomcat}:${password} -T target/*.war http://localhost:7080/manager/text/deploy?path=/mvnpipelines"
                }
            }
        }
    }
}
