def config 
pipeline {
    agent any
    
    parameters {
        booleanParam(defaultValue: false, name: 'DEPLOY', description: 'Build Docker Image and Deploy to Open Shift')
        booleanParam(defaultValue: true, name: 'SONAR_SCAN',  description:  'Enable or Disable Sonar Scan.')
        booleanParam(defaultValue: false, name: 'FORTIFY_SCAN', description: 'Enable or Disable Fortify Scan.')
        choice(choices: ['Dev', 'Test', 'Stage', 'Prod'], description: 'Choose the Environment?', name: 'ENVIRONMENT')
    }
    stages {
        
        stage('prepare') {
            steps {
                script {
                    config = {}
                    echo 'Trigger to build preparation.'
                    config.currentBranch = env.BRANCH_NAME
                    config.enableSonar   = true
                    config.enableFortify = false
                }
            }
        }
       
        stage('Build Stage') {
            steps {
                echo ' Trigger to start the build...  --> '+params.ENVIRONMENT.toLowerCase()
            }
        }
 
        stage('Sonar Stage') {
            when {
                expression {
                    enableSonar(config)
                }
            }
            steps {
                 //Sonar Scan
                script {
                    echo ' Trigger to start the sonar process... '
                }
            }
        }
        
        stage('Upload Artifactory') {
            when {
                expression {
                    params.SONAR_SCAN
                }
            }
            steps {
                 //Artifactory Upload
                script {
                    echo ' Trigger to start the upload Artifactory process... '
                }
            }
        }
            
        stage('Fortify Scan') {
            when {
                expression {
                    enableFortify(config)
                }
            }            
            steps {
                echo 'Trigger to start the fortify process... '
                script {
                    echo 'start fortify scan'
                }
            }
        }

        stage('dev deploy') {
            steps {
                echo 'Trigger to start dev deployment process...'
            }
        }
        
        stage('test deploy') {
            steps {
                echo 'Trigger to start test deployment process...'
            }
        }
        
        stage('stage deploy') {
            steps {
                echo 'Trigger to start stage process...'
            }
        }
        
        stage('prod deploy') {
            steps {
                echo 'Trigger to start  prod process...'
            }
        }
    }
    
    post {
        success {
            echo 'All pipeline stages were successfully invoked.'
        }
        
        failure {
            echo 'Failed to invoke pipeline stages.'
        }
        
        unstable {
            echo 'Build was unstable.'
        }
    }
}

def enableSonar(params) {
    def sonarFlag
    echo 'enableFortify params :: '+params.currentBranch + ' enableFortify :: '+params.enableSonar
    if(params.currentBranch.matches("develop|release-|hotfix-") || params.enableSonar) {
        sonarFlag = true
    }
    sonarFlag
}

def enableFortify(params) {
    def fortifyFlag
    echo 'enableFortify params :: '+params.currentBranch + ' enableFortify :: '+params.enableFortify
    if((params.currentBranch.matches("develop|release-|hotfix-")) || params.enableFortify) {
        fortifyFlag = true
    }    
    fortifyFlag
}
