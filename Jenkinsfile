pipeline {
    agent { 
        label 'alpine'
        }
    stages {
        stage('semgrep') {
            steps {
                script {
                    sh 'apk add python3'
                    sh 'apk add --update pipx'
                    sh 'pipx install semgrep; pipx ensurepath; source ~/.bashrc'
                    sh '/root/.local/bin/semgrep scan --config auto > semgrep.txt'
                    //sh '/root/.local/bin/semgrep ci'
                    archiveArtifacts artifacts: 'semgrep.txt', allowEmptyArchive: true
                    }
                }
            }  
        stage('owasp_zap') {
            steps {
                script {
                sh 'curl -L -o ZAP_2.15.0_Linux.tar.gz https://github.com/zaproxy/zaproxy/releases/download/v2.15.0/ZAP_2.15.0_Linux.tar.gz'
                sh 'tar -xzf ZAP_2.15.0_Linux.tar.gz'
                sh './ZAP_2.15.0/zap.sh -cmd -addonupdate -addoninstall wappalyzer -addoninstall pscanrulesBeta'
                sh './ZAP_2.15.0/zap.sh -cmd -quickurl https://s410-exam.cyber-ed.space:8084 -quickout $(pwd)/zapsh-report.json'
                stash name: 'zapsh-report', includes: 'zapsh-report.json'
                archiveArtifacts artifacts: 'zapsh-report.json', allowEmptyArchive: true
                }
            }
        }
    }
} 
    
