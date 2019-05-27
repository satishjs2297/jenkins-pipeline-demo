pipeline {
    agent any
    
    parameters {
        booleanParam(defaultValue: false, name: 'DEPLOY', description: 'Build Docker Image and Deploy to Open Shift')
        booleanParam(defaultValue: true, name: 'SONAR_SCAN',  description:  'Enable or Disable Sonar Scan.')
        booleanParam(defaultValue: true, name: 'FORTIFY_SCAN', description: 'Enable or Disable Fortify Scan.')
        choice(choices: ['Dev', 'Test', 'Stage', 'Prod'], description: 'Choose the Environment?', name: 'ENVIRONMENT')
        
    }
    stages {
        
        stage('prepare') {
            steps {
                echo 'Trigger to build preparation.'
            }
        }
       
        stage('Build') {
         parallel {
            stage('Maven Build & Sonar') {
                steps {
                    echo ' Trigger to start the build...  --> '+params.ENVIRONMENT.toLowerCase()
    
                    //Artifactory Upload
                    script {
                        echo ' Trigger to start the upload Artifactory process... '
                    }
                    
                    //Sonar Scan
                    script {
                        echo ' Trigger to start the sonar process... '
                    }
                }
            }
            
            stage('Fortify Scan') {
                steps {
                    echo 'Trigger to start the fortify process... '
                    script {
                        echo 'start fortify scan'
                    }
                }
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
