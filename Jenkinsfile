pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                echo '1. Mengambil kode dari GitHub...'
                // Pastikan ID ini sudah benar di Jenkins Credential Anda
                git branch: 'main', 
                    credentialsId: 'github-credential', 
                    url: 'https://github.com/Arief-IF/ci-cd.git' 
            }
        }

        stage('Verification & Deployment') {
            steps {
                echo '2. Mempersiapkan direktori deployment (C:\\staging)...'
                // Ganti: sh 'mkdir -p C:\\staging' -> Menggunakan bat (Windows)
                bat 'if not exist C:\\staging mkdir C:\\staging'

                echo '3. Menyalin index.html ke lokasi deployment...'
                // Ganti: sh 'cp index.html C:\\staging' -> Menggunakan bat copy (Windows)
                bat 'copy index.html C:\\staging' 
                echo "Deployment ke C:\\staging selesai."
            }
        }

        stage('Post-Deployment Test') {
            steps {
                echo '4. Melakukan verifikasi pasca-deployment...'
                // Ganti: sh 'if [ -f... ]' -> Menggunakan bat if exist (Windows)
                bat 'if exist C:\\staging\\index.html ( echo "Verifikasi file SUKSES." ) else ( echo "Verifikasi file GAGAL! File tidak ditemukan." & exit /b 1 )'
                
                echo "Pipeline Deployment Berhasil untuk Build #${env.BUILD_NUMBER}!"
            }
        }
    }

    post {
        always {
            echo "Pipeline Selesai. Status: ${currentBuild.result}"
        }
    }
}
