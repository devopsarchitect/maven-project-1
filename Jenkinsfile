pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '35.172.190.47', description: 'Staging Server')
        
                }

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
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i /var/lib/jenkins/tomcat-demo.pem **/target/*.war ubuntu@${params.tomcat_dev}:/var/lib/tomcat8/webapps"
                    }
                }
            }
        }
    }
}
