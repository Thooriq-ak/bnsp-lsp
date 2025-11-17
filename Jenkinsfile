pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Static HTML - tidak ada proses build.'
            }
        }

        stage('Test') {
            steps {
                echo 'Pseudo-test: list file'
                bat 'dir'
            }
        }

        stage('Deploy to Folder') {
            steps {
                echo 'Copy file ke folder web lokal'
                bat """
                    del /q C:\\deploy\\*
                    xcopy * C:\\deploy\\ /E /Y
                """
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image based on your Dockerfile...'
                bat """
                    docker build -t my-static-web:latest .
                """
            }
        }

        stage('Update Docker Container') {
            steps {
                echo 'Restarting container with new image...'
                bat """
                    docker stop my-web || echo No existing container
                    docker rm my-web || echo No container to remove
                    docker run -d -p 8085:80 --name my-web my-static-web:latest
                """
            }
        }

    }

    post {
        success {
            echo 'Pipeline sukses! Folder dan Docker terupdate.'
        }
        failure {
            echo 'Pipeline gagal! Cek log.'
        }
    }
}
