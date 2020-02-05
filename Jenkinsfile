node {
    stage('Checkout Branch') {
        checkout scm
    }

    docker.image('node:lts').inside('-v npm:/root/.npm/_cacache') {
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

        // stage('Release') {
        //     sh 'npm publish'
        // }

        // stage('Deploy') {
        //     input {
        //         message "Should we continue?"
        //         ok "Yes, we should."
        //     }
        //     steps {
        //         sh 'firebase deploy --token $FIREBASE_TOKEN'
        //     }
        // }
    }
}
