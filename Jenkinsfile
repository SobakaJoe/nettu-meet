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
               sh '/root/.local/bin/semgrep scan --config auto > semgrep_result.json'
               archiveArtifacts artifacts: 'semgrep_result.json', allowEmptyArchive: true
                    }
               }
           }  
        stage('owasp_zap') {
           steps {
               script {
                   sh 'curl -L -o ZAP_2.15.0_Linux.tar.gz https://github.com/zaproxy/zaproxy/releases/download/v2.15.0/ZAP_2.15.0_Linux.tar.gz'
                   sh 'tar -xzf ZAP_2.15.0_Linux.tar.gz'
                   sh './ZAP_2.15.0/zap.sh -cmd -addonupdate -addoninstall wappalyzer -addoninstall pscanrulesBeta'
                   sh './ZAP_2.15.0/zap.sh -cmd -quickurl https://s410-exam.cyber-ed.space:8084 -quickout $(pwd)/zap_result.json'
                   stash name: 'zap_result', includes: 'zap_result.json'
                   archiveArtifacts artifacts: 'zap_result.json', allowEmptyArchive: true
                 }
             }
         }
        stage('trivy') {
            agent {
                label 'dind'
            }
            steps {
                script {
                    sh '''
                    wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
                    echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
                    sudo apt-get update
                    sudo apt-get install trivy
                    trivy repo https://github.com/SobakaJoe/nettu-meet -f json -o trivy_result.json
                    curl -X "POST" -kL "https://s410-exam.cyber-ed.space:8083/api/v2/import-scan/" -H "accept: application/json" -H "Authorization: Token c5b50032ffd2e0aa02e2ff56ac23f0e350af75b4" -H "Content-Type: multipart/form-data" -F "active=true" -F "verified=true" -F "deduplication_on_engagement=true" -F "minimum_severity=High" -F "scan_date=2024-08-31" -F "engagement_end_date=2024-08-31" -F "group_by=component_name" -F "tags=" -F "product_name=exam_larin" -F "file=@trivy_result.json;type=application/json" -F "auto_create_context=true" -F "scan_type=Semgrep JSON Report" -F "engagement=1"
                        '''
                    archiveArtifacts artifacts: 'trivy_result.json', allowEmptyArchive: true      
                }   
            }
        } 
        stage('QG') {
            agent {
                label 'alpine'
            }
         steps { 
             echo 'hello world
         }
    }
}
}    

    
        

