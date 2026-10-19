node {
    stage('Checkout') {
        checkout scm
    }
    stage('Build & Deploy') {
        sh 'docker compose up -d --build'
    }
    stage('Test') {
        sh '''
            for i in $(seq 1 60); do
              curl -sf http://172.16.0.10:8081/ > /dev/null && break
              sleep 2
            done
            curl -sf http://172.16.0.10:8081/ | grep -i "todo"
        '''
    }
}