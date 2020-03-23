pipeline {
    agent any
    stages {
        stage('mkdir') {
            steps {
                echo '==>start mkdir'
                sh 'cd docker && mkdir jenkins_home'
            }
        }
        stage('run') {
            steps {
                echo '==>start run'
                sh 'cd docker && docker-compose down && docker-compose up -d'
            }
        }
        stage('del') {
            steps {
                echo '==>start del'
                sh 'docker rmi $(docker images -q -f dangling=true)'
            }
        }
    }
}