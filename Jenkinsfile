pipeline {
    agent { 
        label 'alpine'
        }
    stages {
       // stage('semgrep') {
        //    steps {
        //        script {
          //          sh 'apk add python3'
            //        sh 'apk add --update pipx'
              //      sh 'pipx install semgrep; pipx ensurepath; source ~/.bashrc'
                //    sh '/root/.local/bin/semgrep scan --config auto > semgrep_result.json'
                  //  archiveArtifacts artifacts: 'semgrep_result.json', allowEmptyArchive: true
                 //   }
               // }
           // }  
       // stage('owasp_zap') {
         //   steps {
          //      script {
            //    sh 'curl -L -o ZAP_2.15.0_Linux.tar.gz https://github.com/zaproxy/zaproxy/releases/download/v2.15.0/ZAP_2.15.0_Linux.tar.gz'
            //  sh 'tar -xzf ZAP_2.15.0_Linux.tar.gz'
            //    sh './ZAP_2.15.0/zap.sh -cmd -addonupdate -addoninstall wappalyzer -addoninstall pscanrulesBeta'
            //    sh './ZAP_2.15.0/zap.sh -cmd -quickurl https://s410-exam.cyber-ed.space:8084 -quickout $(pwd)/zap_result.json'
            //    stash name: 'zap_result', includes: 'zap_result.json'
            //    archiveArtifacts artifacts: 'zap_result.json', allowEmptyArchive: true
            //    }
          //  }
       // }
        stage('trivy') {
            agent {
                label 'dind'
            }
            steps {
                script {
                    sh 'wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -'
                    sh 'echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list'
                    sh 'sudo apt-get update'
                    sh 'sudo apt-get install trivy'
                    sh 'trivy repo https://github.com/SobakaJoe/nettu-meet -f json -o json > trivy_result.json'
                    archiveArtifacts artifacts: 'trivy_result.json', allowEmptyArchive: true
                    
                    
                }   
            }
        } 
    }
}

