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
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://192.168.1.64:9000 -Dsonar.token=sqp_403c50208d088cfc95b793ecbff657f61358afa4"
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
