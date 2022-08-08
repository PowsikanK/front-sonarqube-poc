pipeline {
    agent any
    tools{
        nodejs "node"
    }
    stages {
        stage('Build') {
            steps {
    		    sh "npm install"
                sh "npm run build"
            }
        }
         stage('SonarQube Analysis') {
            steps {
                script {
                    // requires SonarQube Scanner 2.8+
                    scannerHome = tool 'sonarqube'
                }
                withSonarQubeEnv(installationName: 'sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
            
    }
}
