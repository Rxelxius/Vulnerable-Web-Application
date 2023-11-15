pipeline {
    agent any
    stages {
        stage ('Checkout') {
        steps {
            git branch:'master', url: 'https://github.com/Rxelxius/Vulnerable-Web-Application.git'
        }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://sonarqube:9000 -Dsonar.token=sqp_04269f86e190336e4070bf9b8d1a0c7311dce211"
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}
