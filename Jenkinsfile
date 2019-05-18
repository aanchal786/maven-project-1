pipeline {
    agent any
 
    tools {
        maven 'localmvn'
    }

    parameters {
         string(name: 'Tomcat_staging', defaultValue: '172.31.95.119', description: 'Staging Server')
         string(name: 'Tomcat_prod', defaultValue: '172.31.81.150', description: 'Production Server')
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
                        sh "scp -v -o StrictHostKeyChecking=no -i /home/ec2-user/Jenkins.pem **/target/*.war ec2-user@${params.Tomcat_staging}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -v -o StrictHostKeyChecking=no -i /home/ec2-user/Jenkins.pem **/target/*.war ec2-user@${params.Tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}
