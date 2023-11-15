pipeline {
    agent any
        stages {
            

            stage('Build') { 
                steps {
                    sh 'npm install' 
                }
            }

            stage('Code Quality Check via Sonarqube') {
                steps {
                    script {
                            def scannerHome = tool 'Sonarqube';
                            withSonarQubeEnv('Sonarqube') {
                                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=."
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
