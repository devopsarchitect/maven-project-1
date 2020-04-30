pipeline {
    agent any

    triggers {
         pollSCM('* * * * *')
     }

	stages{
			stage('Build'){
				steps {
					sh 'mvn clean package'
				}
				post {
					success {
						echo 'Now Archiving...'
						archiveArtifacts artifacts: '**/target/*.war'
					}
				}
			}

			stage ('Deployments'){
					
				steps ('Deploy to Staging'){
						
					sshagent(['tpsystemsarchitect']) {
						sh 'scp -o StrictHostKeyChecking=no target/*.war tpsystemsarchitect@34.68.242.174:/opt/bitnami/apache-tomcat/webapps'
					}				

				   
				}
			}
		}
	
	}