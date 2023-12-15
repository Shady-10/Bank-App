def COLOR_MAP = [
    'SUCCESS' : 'good',
    'FAILURE' : 'danger',
]

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


        // // Stage Two (Install Dependencies For Root With NPM)

        // stage('Root Dependencies'){

        //     steps{
                
        //         sh 'npm install'
        //     }
        // }

        // // Stage Three (Install Dependencies For The Backend With NPM)

        // stage('Backend Dependencies'){

        //     steps{

        //         dir('${JENKINS_HOME/workspace/Bank-App/app/backend'){
        //             sh 'npm install'
        //         }
        //     }
        // }

        // // Stage Four (Install Dependencies For The Frontend With NPM)

        // stage('Frontend Dependencies'){

        //     steps{

        //         dir('${JENKINS_HOME/workspace/Bank-App/app/frontend'){
        //             sh 'npm install'
        //         }
        //     }
        // }

         // Stage Five (Performing OWASP Analysis)

        // stage('OWASP Analysis'){
        //     steps{
        //         dependencyCheck additionalArguments: '-s ./' , odcInstallation: 'DC'
        //         dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        //     }
        // }

        // Stage Six (Trivy Analysis)

        stage('Trivy'){

            steps{

                sh 'trivy fs .'
            }
        }

        // Stage Seven (SonarQube Scan)

        // stage('SonarQube'){

        //     environment{
        //         scannerHome = tool 'SONAR4.7'
        //     }

        //     steps{
        //         withSonarQubeEnv('SONAR'){
        //             sh ''' ${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=Bank \
        //             -Dsonar.projectName=Bank \
        //             -Dsonar.projectVersion=1.0'''
        //         }
        //     }
        // }

        // Stage Eight (Quality Gate)

        // stage('Quality Gate Check'){

        //     steps{

        //         timeout(time: 8 , unit: 'MINUTES'){

        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }
        // // Stage Nine (Docker)

        // stage('Docker'){

        //     steps{

        //         sh 'npm run compose:up -d'
        //     }
        // }
    }

    // post{
    //     always{
    //         echo 'Slack Notifications .'
    //         slackSend channel: '#jenkinscicd',
    //             color: COLOR_MAP[currentBuild.currentResult],
    //             message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
    //     }
    // }
}