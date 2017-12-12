pipeline {
    agent { label 'master' }

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Init') {
            steps {
                echo "Initializing"
            }
        }

        stage('Deploy to CI') {
            agent { label 'deployer01' }
            steps {
                sh '/home/magagan/deploymentScripts/deployStagingOnewebDistributed.sh $GIT_COMMIT'
            }
        }

        stage('Staging Testing') {
            parallel {
                stage ('S-RS-04-AdSenseListing-AdsenseDetails-AudienceSegments-AdUnits') {
                    steps {
                        echo 'test1'
                    }
                }

                stage ('S-RS-05-SellForm') {
                    steps {
                        echo 'test2'
                    }
                }

                stage ('S-RS-01-HomePage-Listings-Details') {
                    steps {
                        echo 'test3'
                    }
                }

                stage ('S-RS-02-Login-Registration-CategoryLinks') {
                    steps {
                        echo 'test4'
                    }
                }

                stage ('S-RS-03-TopUp-VasRefresh-AdBoostingPackage') {
                    steps {
                        echo 'test5'
                    }
                }
            }
        }

        stage ('Deploy to Production'){
            agent { label 'deployer01' }
            steps{

                input message:'Approve PRODUCTION Deployment?'

                echo 'sleeping 20s'
                sh 'sleep 20s'
                echo 'done sleeping'
            }
            post {
                success {
                    echo 'Changes deployed to Production.'
                }

                failure {
                    echo 'Deployment failed.'
                }
            }
        }
    }
}