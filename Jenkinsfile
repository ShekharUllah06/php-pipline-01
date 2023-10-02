pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // Run Phing to build your PHP project
                sh 'phing'
            }
        }
        stage('Deploy') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                script {
                    def webRoot = '/var/www/html'
                    def projectDir = 'phpprojects/p1'
                    def deployDir = "${webRoot}/${projectDir}"
                    
                    sh "mkdir -p ${deployDir}"
                    sh "cp -r ./* ${deployDir}"
                    
                    echo "Deployment successful!"
                }
            }
        }
    }
    post {
        success {
            // Add any post-build actions for a successful build here
            echo "Build was successful!"
        }
        failure {
            // Add any post-build actions for a failed build here
            echo "Build failed. Deployment will not be executed."
        }
    }
}
