pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Deploy Backends') {
    steps {
        sh '''
        docker network create mynetwork || true
        docker rm -f backend1 backend2 || true
        docker run -d --name backend1 --network mynetwork backend-app
        docker run -d --name backend2 --network mynetwork backend-app
        sleep 3
        '''
    }
}

        stage('Start Nginx') {
    steps {
        sh '''
        docker rm -f nginx-lb || true
        docker run -d -p 80:80 --name nginx-lb --network mynetwork nginx
        sleep 2
        docker cp nginx/default.conf nginx-lb:/etc/nginx/conf.d/default.conf
        docker exec nginx-lb nginx -s reload
        '''
    }
}
    }
}
