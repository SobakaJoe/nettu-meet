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
                    sh 'pwd'
                    sh 'ls'
                    sh 'cd server'
                    sh 'ls'
                    sh 'docker build -t nettu-meet-server:latest -f server/Dockerfile'
                    // sh 'docker pull bitnami/trivy:latest'
                    // sh' cd sever'
                    // sh 'docker build -t nettu-meet-server:latest -f Dockerfile'
                    // sh 'trivy image --format cyclonedx --output sbom_server.json nettu-meet-server:latest'
                    // sh 'docker build ./frontend/docker -t nettu-meet-front:latest -f Dockerfile'
                    // sh 'trivy image --format cyclonedx --output sbom_frontend.json nettu-meet-frontend:latest'
                    // archiveArtifacts artifacts: 'sbom_server.json', allowEmptyArchive: true
                    // archiveArtifacts artifacts: 'sbom_frontend.json', allowEmptyArchive: true
                }   
            }
        } 
    }
}
    
