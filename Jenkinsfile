pipeline {
    agent any
    stages {
        stage('SAST') {
            steps {
                // Сканирование кода с использованием Semgrep
                semgrep(
                    tool: 'semgrep',
                    pattern: '^security_rules$',
                    failOnAlert: true,
                    severityThreshold: 'high'
                )
            }
        }
    }
}
