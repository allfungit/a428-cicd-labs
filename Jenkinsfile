    pipeline {
        agent {
            docker {
                image 'node:16-buster-slim' 
                args '-p 4000:4000' 
            }
        }
        stages {
            stage('Build') { 
                steps {
                    sh 'npm install' 
                }
            }
            stage('Test') {
                steps {
                    sh './jenkins/scripts/test.sh'
                }
            }
            stage('Manual Approval') {
                steps {
                    input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan atau "Abort" untuk berhenti)'
                }
            }
            stage('Deploy') {
                steps {
                    sh './jenkins/scripts/deliver.sh'
                    sleep time: 1, unit: 'MINUTES'
                    sh './jenkins/scripts/kill.sh'
            }
        }
        }
    }
