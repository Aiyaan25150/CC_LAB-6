pipeline {
    agent any

    stages {
        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-image ./backend'
            }
        }

        stage('Run Backend Container') {
            steps {
                sh 'docker run -d --name backend-container backend-image'
            }
        }

        stage('Run Nginx') {
            steps {
                sh 'docker run -d -p 80:80 --name nginx-container -v $PWD/nginx/default.conf:/etc/nginx/conf.d/default.conf nginx'
            }
        }
    }
}
