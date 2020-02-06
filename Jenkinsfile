node {
    stage('Checkout Branch') {
        checkout scm
    }

    docker.image('circleci/node:latest-browsers').inside('-v npm:/root/.npm/_cacache') {
        stage('Install Dependencies') {
            sh 'npm ci'
        }

        parallel 'Linting': {
            stage('Linting') {
                sh 'npm run lint'
            },
            'Test': {
                stage('Test') {
                sh 'npm run test:ci'
                }
            },
            'Build': {
                stage('Build') {
                    sh 'npm run build'
                }
            }
        }

        stage('Release') {
            sh 'npm publish --registry localhost:4873'
        }

        stage('Deploy') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
            }
            steps {
                sh 'firebase deploy --token $FIREBASE_TOKEN'
            }
        }
    }
}
