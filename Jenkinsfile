pipeline {
    agent any

   // parameters {
   //      string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
   //      string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
   //

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
					sshagent(['tpsystemsarchitect']) {
					// some block
                       sh 'scp -o StrictHostKeyChecking=no target/*.war tpsystemsarchitect@34.68.242.174:/opt/bitnami/apache-tomcat/webapps'
                    }
                }

           //   stage ("Deploy to Production"){
           //       steps {
       //               sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war c2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
            //      }
               //
           //    }
    }
}