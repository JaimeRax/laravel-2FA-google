pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio desde Git
                git credentialsId: 'ssh-credentials-id', git branch: 'main', url: 'git@github.com:JaimeRax/laravel-2FA-google.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Instalar dependencias de PHP usando Composer
                sh 'composer install --no-interaction --prefer-dist --optimize-autoloader'
            }
        }

        stage('Run Tests') {
            steps {
                // Ejecutar las pruebas de PHPUnit
                sh './vendor/bin/phpunit'
            }
        }

        stage('Dependency Track Analysis') {
            steps {
                script {
                    // Verificar si Dependency Track está instalado
                    sh 'which dependency-track || { echo "Dependency Track not found"; exit 1; }'

                    // Ejecutar Dependency Track para analizar las dependencias
                    sh 'dependency-track --project d11f0baf-29b4-4035-9110-b484c2018f5f --api-key odt_YMvH1o1YLuHFLBPovCCd22eli4QqcONb --file dependency-track-results.json'
                }
            }
        }

        stage('Generate Report') {
            steps {
                script {
                     // Verificar si jq y pandoc están instalados
                    sh 'which jq || { echo "jq not found"; exit 1; }'
                    sh 'which pandoc || { echo "Pandoc not found"; exit 1; }'

                    // Crear un archivo Markdown con los resultados del análisis
                    sh '''
                    echo "# Dependency Track Vulnerability Report" > report.md
                    echo "" >> report.md
                    echo "## Vulnerabilities" >> report.md

                    cat dependency-track-results.json | jq -r ".vulnerabilities[] | \"### \\(.name)\\nSeverity: \\(.severity)\\nDescription: \\(.description)\\nRecommendations: \\(.recommendations)\\n\"" >> report.md

                    # Convertir Markdown a PDF usando Pandoc
                    pandoc report.md -o report.pdf
                    '''
                }
            }
        }

        stage('Archive Report') {
            steps {
                // Archivar el reporte generado como artefacto en Jenkins
                archiveArtifacts artifacts: 'report.pdf', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Limpieza y notificaciones (si es necesario)
            cleanWs()
        }
    }
}
