pipeline {
    agent { label 'master' }
    stages {
        stage('Initialized') {
            steps {
                echo "Initializing"
            }
        }

        stage('Deploy to CI') {
            agent { label 'deployer01' }
            steps {
                sh '/home/magagan/deploymentScripts/deployStagingOnewebDistributed.sh'
            }
        }

        stage('Testing') {
            steps {
                build job: 'S-RS-04-AdSenseListing-AdsenseDetails-AudienceSegments-AdUnits'
            }

            steps {
                build job: 'S-RS-05-SellForm'
            }
        }

    }
}