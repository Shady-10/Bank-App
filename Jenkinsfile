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
                    sh ''' ${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=Bank \
                    -Dsonar.projectName=Bank \
                    -Dsonar.projectVersion=1.0'''
                }
            }
        }

        // Stage Five (Install Dependencies For Root With NPM)

        stage('Root Dependencies'){

            steps{
                
                sh 'npm install'
            }
        }

        // Stage Six (Install Dependencies For The Backend With NPM)

        stage('Backend Dependencies'){

            steps{

                dir('/root/.jenkins/workspace/Bank-App/app/backend'){
                    sh 'npm install'
                }
            }
        }

        // Stage Seven (Install Dependencies For The Frontend With NPM)

        stage('Backend Dependencies'){

            steps{

                dir('/root/.jenkins/workspace/Bank-App/app/frontend'){
                    sh 'npm install'
                }
            }
        }

        // Stage Eight (Deploying Docker Containers)

        stage('Docker'){

            steps{

                sh 'npm run compose:up -d'
            }
        }
    }
}