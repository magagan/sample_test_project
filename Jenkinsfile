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
            agent { label 'reg-server04' }
            steps {
                build job: 'S-RS-04-AdSenseListing-AdsenseDetails-AudienceSegments-AdUnits'
            }

            agent { label 'reg-server05' }
            steps {
                build job: 'S-RS-05-SellForm'
            }
        }

    }
}