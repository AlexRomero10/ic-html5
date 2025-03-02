pipeline {
    agent {
        docker { 
            image 'josedom24/debian-npm'
            args '--env TOKEN=$SURGE_TOKEN -u root:root'
        }
    }
    environment {
        SURGE_TOKEN = credentials('SURGE_TOKEN')
    }
    stages {
        stage('Clone') {
            steps {
                git branch: 'master', url: 'https://github.com/AlexRomero10/ic-html5.git'
            }
        }
        
        stage('Install surge') {
            steps {
                sh 'npm install -g surge'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'surge ./_build/ alejandro24.surge.sh --token $SURGE_TOKEN'
            }
        }
    }
}
