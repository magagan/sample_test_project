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
                sh '/home/magagan/deploymentScripts/deployStagingOnewebDistributed.sh $GIT_COMMIT'
            }
        }

        stage('Staging Testing') {
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

                stage ('S-RS-01-HomePage-Listings-Details') {
                    steps {
                        build job: 'S-RS-01-HomePage-Listings-Details'
                    }
                }

                stage ('S-RS-02-Login-Registration-CategoryLinks') {
                    steps {
                        build job: 'S-RS-02-Login-Registration-CategoryLinks'
                    }
                }

                stage ('S-RS-03-TopUp-VasRefresh-AdBoostingPackage') {
                    steps {
                        build job: 'S-RS-03-TopUp-VasRefresh-AdBoostingPackage'
                    }
                }
            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout(time:10, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'oneweb-prod-deploy'
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

        stage('Production Testing') {
            parallel {
                stage ('P-RS-04-AdSenseListing-AdsenseDetails-AudienceSegments-AdUnits') {
                    steps {
                        build job: 'P-RS-04-AdSenseListing-AdsenseDetails-AudienceSegments-AdUnits'
                    }
                }

                stage ('P-RS-05-SellForm') {
                    steps {
                        build job: 'P-RS-05-SellForm'
                    }
                }

                stage ('S-RS-01-HomePage-Listings-Details') {
                    steps {
                        build job: 'P-RS-01-HomePage-Listings-Details'
                    }
                }

                stage ('S-RS-02-Login-Registration-CategoryLinks') {
                    steps {
                        build job: 'P-RS-02-Login-Registration-CategoryLinks'
                    }
                }

                stage ('P-RS-03-TopUp-VasRefresh-AdBoostingPackage') {
                    steps {
                        build job: 'P-RS-03-TopUp-VasRefresh-AdBoostingPackage'
                    }
                }
            }
        }
    }
}