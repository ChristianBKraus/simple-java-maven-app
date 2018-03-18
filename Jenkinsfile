pipeline {
    agent {
        docker 
    }
    stages {
    
        stage('build') { 
           node('docker&&windows'){ 
               bat 'echo NodeName = %COMPUTERNAME%' 
               docker.image('microsoft/windowsservercore:10.0.14393.206').inside { 
                   bat 'echo %COMPUTERNAME% > container_computername.txt' 
               } 
           } 
        }
               
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                bat './jenkins/scripts/deliver.sh'
            }
        }
    }
}
