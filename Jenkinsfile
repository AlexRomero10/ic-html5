pipeline {
    agent {
        docker {
            image 'josedom24/debian-npm'
            args '-u root:root'
        }
    }
   
    environment {
        TOKEN = credentials('SURGE_TOKEN')
    }
   
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/AlexRomero10/ic-html5.git'
            }
        }
       
        stage('Change Repositories to HTTPS') {
            steps {
                sh '''
                sed -i 's/http:/https:/g' /etc/apt/sources.list
                apt update
                '''
            }
        }
       
        stage('Install Surge') {
            steps {
                sh 'npm install -g surge'
            }
        }
       
        stage('Install Dependencies') {
            steps {
                sh 'apt update -y && apt install -y python3-pip default-jre'
                sh 'pip3 install html5validator'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'surge ./_build/ alejandro24.surge.sh --token $TOKEN'
            }
        }
    }
}
