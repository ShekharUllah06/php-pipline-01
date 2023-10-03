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
                // Run build commands for your PHP project
                sh 'composer install'  // Example: Install PHP dependencies using Composer
                sh 'phpunit'           // Example: Run PHPUnit tests
                // Add more build steps as needed
            }
        }
        stage('Deploy') {
            steps {
                // Copy the built project files to the deployment directory
                script {
                    def webRoot = '/var/www/html'
                    def projectDir = 'phpprojects/p1'
                    def deployDir = "${webRoot}/${projectDir}"

                    sh "mkdir -p ${deployDir}"
                    sh "cp -r ./* ${deployDir}"
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
