pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps work too"
                    ls -lah
                '''
            }
        }

        stage('Snyk Test') {
            steps {
                script {
                    // Install Snyk CLI
                    sh 'npm install -g snyk'

                    // Authenticate and test
                    withCredentials([string(credentialsId: 'snyk', variable: 'SNYK_TOKEN')]) {
                        sh 'snyk auth $SNYK_TOKEN'
                        sh 'snyk test'
                    }
                }
            }
        }


        stage('Upload to AWS') {
            steps {
                withAWS(region: 'us-east-1', credentials: 'aws-cred') {
                    sh 'echo "Uploading content with AWS creds"'

                    // Upload multiple files to S3
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'components.html', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'main.bc58148c.js.gz', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'assets', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'sample', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'main.bc58148c.js', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'main.bc58148c.map', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'main.d8e0d294.css', bucket: 'static5533')
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'main.d8e0d294.css.gz', bucket: 'static5533')
                }
            }
        }
    }
}
