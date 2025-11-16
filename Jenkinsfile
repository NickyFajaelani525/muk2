pipeline {
    agent any // Menjalankan di agent (node) mana saja yang tersedia

    stages {
        stage('Build') {
            // Untuk file statis .html, tidak ada proses 'build'
            steps {
                echo 'File kopika.html adalah file statis, tidak perlu build.'
            }
        }

        stage('Test') {
            // Tidak ada tes otomatis untuk file HTML sederhana
            steps {
                echo 'Tidak ada proses testing untuk MUK ini.'
            }
        }

        stage('Deploy to EC2 Target') {
            steps {
                echo 'Memulai proses deploy ke Server Target...'
                
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-server-key', keyFileVariable: 'SSH_KEY', usernameVariable: 'SSH_USER')]) {
                    
                    echo "Mengirim kopika.html ke ${SSH_USER}@47.128.191.147:/var/www/html/"
                    
                    sh "scp -o StrictHostKeyChecking=no -i ${SSH_KEY} kopika.html ${SSH_USER}@47.128.191.147:/var/www/html/"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline BERHASIL nih ngab. File kopika.html sudah ter-deploy.'
            echo 'Akses di: http://47.128.191.147/kopika.html'
        }
        failure {
            echo 'Pipeline GAGAL ni wok.'
        }
    }
}
