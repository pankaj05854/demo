pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    

    stages {
            stage('Deliver for development') {
                        when {
                            expression { params.gitbranch == 'dev' }
                        }
                        steps {
                            sh 'sh /opt/deploy/a.sh dev'
                        }
                    }
            stage('Deploy for test') {
                        when {
                            expression { params.gitbranch == 'test' }
                        }
                        steps {
                            sh 'sh /opt/deploy/a.sh test'
                        }
                    }

            stage('Deploy for stage') {
                        when {
                            expression { params.gitbranch == 'stage' }
                        }
                        steps {
                            sh 'sh /opt/deploy/a.sh stage'
                        }
                    }

            stage('Deploy for security') {
                        when {
                            expression { params.gitbranch == 'security' }
                        }
                        steps {
                            sh './jenkins/scripts/deploy-for-production.sh'
                            input message: 'Finished using the web site? (Click "Proceed" to continue)'
                            sh './jenkins/scripts/kill.sh'
                        }
                    }

            stage('Deploy for prod') {
                        when {
                            expression { params.gitbranch == 'prod' }
                        }
                        steps {
                            sh './jenkins/scripts/deploy-for-production.sh'
                            input message: 'Finished using the web site? (Click "Proceed" to continue)'
                            sh './jenkins/scripts/kill.sh'
                        }
                    }

    }
}

