pipeline
{
	agent {
        label 'Slave_Mac'
    }
	
	tools {
        jdk 'JDK8_Mac'
    }
	
	stages{
		stage('Checkout') {
			steps{
				echo "------------>Checkout<------------"
			}
		}
		
		stage('Compile & Unit Tests') {
			steps{
				echo "------------>>Clean<------------"
				sh './gradlew clean'

				echo "------------>Unit Tests<------------"
				sh './gradlew test'
			}
		}

		stage('Static Code Analysis')
		{
            steps{
                echo '------------>Static Code Analysis<------------'
                withSonarQubeEnv('Sonar') {
                    sh "${tool name: 'SonarScanner', type:'hudson.plugins.sonar.SonarRunnerInstallation'}/bin/sonar-scanner"
                }
             }
        }

	}
	
	post {
		always {
		  echo 'This will always run'
		}
		success {
		  echo 'This will run only if successful'
		  junit 'build/test-results/test/*.xml' → RUTA DE TUS ARCHIVOS .XML
		}
		failure {
		  echo 'This will run only if failed'
		}
		unstable {
		  echo 'This will run only if the run was marked as unstable'
		}
		changed {
		  echo 'This will run only if the state of the Pipeline has changed'
		  echo 'For example, if the Pipeline was previously failing but is now successful'
		}
	}


}