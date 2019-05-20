pipeline {
    agent any
    tools {
        maven 'localmvn'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
                sh "docker build . -t Tomcat_webapp:${env.Build_ID}"
            }
        }
    }
}
