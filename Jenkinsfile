pipeline {
    agent any

    environment {
        PATH = "C:\\Program Files\\Docker\\Docker\\resources\\bin;C:\\Program Files\\Git\\bin;C:\\Windows\\System32"
        IMAGE_NAME = "vize"
        CONTAINER_NAME = "vize"
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Repoyu Klonla') {
            steps {
                git branch: 'main', url: 'https://github.com/Beyzacicekay/YMGVIZESINAVI.git'
            }
        }

        stage('Docker Image Oluştur') {
            steps {
                echo "Docker image oluşturuluyor..."
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Eski Docker\'ı Durdur') {
            steps {
                echo "Eski docker container durduruluyor..."
                bat "docker rm -f %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Yeni Container Oluştur') {
            steps {
                echo "Yeni docker container başlatılıyor..."
                bat "docker run -d --name %CONTAINER_NAME% -p 5050:80 %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo " Başarılı!"
        }
        failure {
            echo " Başarısız!"
        }
    }
}

