def secret = 'sshgit'
def vmapps = 'imronvin@10.148.0.5'
def dir = '/home/imron/dumbflix-frontend'
def branch = 'master'

pipeline {
    agent any

    stages {
        stage("pull") {
            steps {
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${vmapps} << EOF
cd ${dir}
git pull origin ${branch}
echo "Git Pull Telah Selesai"
exit
EOF
"""
                }
            }
        }

        stage("build") {
            steps {
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${vmapps} << EOF
cd ${dir}
npm install
echo "Installation dependencies telah selesai"
exit
EOF
"""
                }
            }
        }

        stage("run") {
            steps {
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${vmapps} << EOF
cd ${dir}
pm2 start ecosystem.config.js
echo "Aplikasi telah dijalankan dengan PM2"
exit
EOF
"""
                }
            }
        }
    }
}
