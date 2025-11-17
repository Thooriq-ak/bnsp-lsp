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

        stage('Deploy') {
            steps {
                echo 'Copy file ke folder web lokal'
                bat """
                    del /q C:\\deploy\\*
                    xcopy * C:\\deploy\\ /E /Y
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline sukses!'
        }
        failure {
            echo 'Pipeline gagal!'
        }
    }
}
