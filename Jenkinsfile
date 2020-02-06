node {
    stage('Checkout Branch') {
        checkout scm
    }

    docker.image('circleci/node:latest-browsers').inside('-v npm:/root/.npm/_cacache') {
        stage('Install Dependencies') {
            sh 'npm ci'
        }

        stage('Linting') {
            sh 'npm run lint'
        }

        stage('Test') {
            sh 'npm run test:ci'
        }

        stage('Build') {
            sh 'npm run build'
        }
    }

    stage('Deploy') {
        input message 'Should we continue?'
        steps {
            echo "Now I would deploy to production"
        }
    }
}
