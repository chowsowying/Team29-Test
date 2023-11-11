pipeline {
    agent none
    stages {
        stage('Checkout SCM') {
            agent any
            steps {
                git branch: 'main', url: 'https://github.com/chowsowying/Team29-Test.git'
            }
        }

        // stage('OWASP DependencyCheck') {
        //     agent any
        //     steps {
        //         dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
		// 		dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        //     }
        // }

		  stage('SonarQube Analysis') {
			agent any
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=Team29 -Dsonar.sources=."
                    }
                }
            }

            post {
                always {
                    recordIssues enabledForFailure: true, tool: sonarQube()
                }
            }
        }




      
    }
}
