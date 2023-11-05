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
        sh 'mvn clean package'
    }
}

        stage('Deploy') {
            steps {
                // Deploy war/ear to Tomcat server
                withCredentials([
                    usernamePassword(credentialsId: 'TomcatCreds', usernameVariable: 'tomcat', passwordVariable: 'password')
                ]) {
                   deploy contextPath: 'mvnPipeline', war: '**/*.war'
                }
            }
        }
    }
}
