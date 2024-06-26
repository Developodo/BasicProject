pipeline {
    agent any

    environment {
        FTP_HOST = 'apache-ftp'
        FTP_USER = 'user'
        FTP_PASS = 'password'
        FTP_DIR = './app'
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
  // Utilizar ncftp para transferir archivos al servidor FTP
sh '''
			cd build
                        ncftpput -R -v -u ${FTP_USER} -p ${FTP_PASS} ${FTP_HOST} ${FTP_DIR} .
                    '''
		}
            }
        }
    }
}

