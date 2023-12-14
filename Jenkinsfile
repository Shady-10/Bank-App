pipeline{

    agent any 

    tools{
        jdk 'OracleJDK11'
        nodejs 'Node16'
    }
    stages{

        // Stage One (Pulling The Code From GitHub Repo)
        stage('Fetching code'){

            steps{
                git branch: 'main' , url: 'https://github.com/Shady-10/Bank-App.git'
            }
        }

        // Stage two (Performing OWASP Analysis)

        stage('OWASP Analysis'){

            steps{
                dependencyCheck additionalArguments: '-s ./' , odcInstallation: 'DC'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }

        // Stage Three (Trivy Analysis)

        stage('Trivy'){

            steps{

                sh 'trivy fs .'
            }
        }

        // Stage Four (SonarQube Scan)

        stage('SonarQube'){

            environment{
                scannerHome = tool 'SONAR4.7'
            }

            steps{
                withSonarQubeEnv('SONAR'){
                    sh ''' ${scannerhome}/bin/sonar-scanner -Dsonar.projectKey=Bank \
                    -Dsonar.projectName=Bank \
                    -Dsonar.projectVersion=1.0'''
                }
            }
        }
    
    }
}