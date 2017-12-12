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

        stage('Parallel Testing') {
            parallel {
                stage ('S-RS-04-AdSenseListing-AdsenseDetails-AudienceSegments-AdUnits') {
                    steps {
                        build job: 'S-RS-04-AdSenseListing-AdsenseDetails-AudienceSegments-AdUnits'
                    }
                }

                stage ('S-RS-05-SellForm') {
                    steps {
                        build job: 'S-RS-05-SellForm'
                    }
                }
            }
        }
    }
}