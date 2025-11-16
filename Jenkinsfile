pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                // Ganti dengan ID kredensial, URL, dan nama branch Anda
                git branch: 'main', 
                    credentialsId: 'github-credential', 
                    url: 'https://github.com/Arief-IF/ci-cd.git'
            }
        }

        stage('Verification & Deployment') {
            steps {
                echo '1. Memverifikasi file HTML...'
                // Langkah verifikasi sederhana
                sh 'ls -l index.html' 

                echo '2. Simulasi Deployment...'
                // Gunakan perintah shell untuk menempatkan file di lokasi deployment (misal: C:\staging)
                // (Asumsi: Anda menjalankan Jenkins di Windows, jadi ini akan dijalankan di lingkungan Windows/Container host)
                sh 'mkdir -p C:\\staging'
                sh 'cp index.html C:\\staging'
                sh 'echo "Deployment ke C:\\staging/index.html selesai."'
            }
        }

        stage('Post-Deployment Test') {
            steps {
                // Tes sederhana untuk memverifikasi file ada di lokasi deployment
                sh 'if [ -f C:\\staging/index.html ]; then echo "Verifikasi file SUKSES."; else exit 1; fi'
            }
        }
    }

    post {
        always {
            echo "Pipeline Selesai. Status: ${currentBuild.result}"
        }
    }
}
