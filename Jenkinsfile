pipeline 
{
    agent any
    stages 
    {
        stage ('Checkout') 
        {
            steps 
            {
                git branch: 'main', url: 'https://github.com/SIT-EddieTan/Vulnerable-Web-Application.git'
            }
        }
        stage('Code Quality Check via SonarQube') 
        {
            steps 
            {
                script 
                {
                    def scannerHome = tool 'SonarQube';
                    // Print the path of SonarQube scanner
                    sh "echo SonarQube Scanner Path: ${scannerHome}"

                    withSonarQubeEnv('SonarQube') 
                    {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://172.30.141.239:9000 -Dsonar.token=sqp_391899e639a3cd388703213f14dea621453f0d5e"
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
