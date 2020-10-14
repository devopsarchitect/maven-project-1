pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '18.234.217.143', description: 'Staging Server')
        
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
                        sh "pwd"
                        sh "scp -i /var/snap/jenkins/1416/jobs/Pipeline-as-Code-maven-project-0.4-tag/workspace/tomcat-demo.pem **/target/*.war ubuntu@${params.tomcat_dev}:/var/lib/tomcat8/webapps"
                    }
                }
            }
        }
    }
}
