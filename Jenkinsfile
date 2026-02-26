pipeline {
    agent any

    stages {
        stage('Run Backend Container') {
    steps {
        sh '''
        docker rm -f backend-container || true
        docker run -d --name backend-container backend-image
        '''
    }
}
        stage('Run Backend Container') {
            steps {
                sh 'docker run -d --name backend-container backend-image'
            }
        }

        stage('Run Nginx') {
            steps {
                sh '''
                docker rm -f nginx-container || true
                docker run -d -p 80:80 \
                --name nginx-container \
                -v $(pwd)/nginx:/etc/nginx/conf.d \
                nginx
                '''
            }
        }
    }
}
