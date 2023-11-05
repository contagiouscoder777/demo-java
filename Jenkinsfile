pipeline{
	agent any
	tools{
		maven 'MAVEN_HOME'
	}

	stages{
		stage ('Build'){
			steps{
				sh 'mvn clean package'
			}
			post{
				success{
					echo "Archiving the artifacts"
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		stage ('Deploy to tomcat server'){
			steps{
				deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://localhost:7080')], contextPath: 'mvnPipeline', war: '**/*.war'
			}
		}
	}
}
