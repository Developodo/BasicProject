pipeline {
    agent any

    environment {
        FTP_HOST = 'apache-ftp'
        FTP_USER = 'user'
        FTP_PASS = 'password'
        FTP_DIR = '/var/ftp'
    }

    stages {
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Utilizar lftp para transferir archivos al servidor FTP
                    sh """
                        lftp -e "
                        open -u $FTP_USER,$FTP_PASS $FTP_HOST;
                        mirror -R ./build $FTP_DIR;
                        bye
                        "
                    """
                }
            }
        }
    }
}

