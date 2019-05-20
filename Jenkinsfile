pipeline {
    agent any
    tools {
        maven 'localmvn'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
