pipeline {
    agent any
    
    parameters {
        booleanParam(defaultValue: false, name: 'Deploy', description: 'Build Docker Image and Deploy to Open Shift')
        choice(choices: ['Dev', 'Test', 'Stage', 'Prod'], description: 'Choose the Environment?', name: 'ENVIRONMENT')
        
    }
    stages {
        stage('build') {
            steps {
                echo 'build process... testing :: - '+params.ENVIRONMENT.toLowerCase()
            }
        }
        
        stage('sonar') {
            steps {
                echo 'sonar process... testing'
            }
        }
        
        stage('fortify') {
            steps {
                echo 'fortify process... testing'
            }
        }
        
        stage('upload artifactory') {
            steps {
                echo 'upload process... testing'
            }
        }
        
        stage('dev deploy') {
            steps {
                echo 'dev process... testing'
            }
        }
        
        stage('test deploy') {
            steps {
                echo 'test process... testing'
            }
        }
        
        stage('stage deploy') {
            steps {
                echo 'stage process... testing'
            }
        }
        
        stage('prod deploy') {
            steps {
                echo 'prod process... testing'
            }
        }
    }
}
