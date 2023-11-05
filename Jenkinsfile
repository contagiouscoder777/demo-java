pipeline {
    agent any

    tools {
        // Define your Maven installation here
        maven 'MAVEN_HOME' // Replace 'MAVEN_HOME' with the actual name of your Maven tool
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Use 'sh' to run Maven goals
                    sh 'mvn clean package'
                }
            }
            post {
                success {
                    echo "Archiving the artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to Tomcat server') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://localhost:7080/')], contextPath: 'mvnPipeline', war: '**/*.war'
            }
        }
    }
}
