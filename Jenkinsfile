pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio desde Git
                git branch: 'main', url: 'https://github.com/JaimeRax/laravel-2FA-google'
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
                // Ejecutar Dependency Track para analizar las dependencias
                sh '''
                dependency-track --project d11f0baf-29b4-4035-9110-b484c2018f5f --api-key odt_YMvH1o1YLuHFLBPovCCd22eli4QqcONb --file dependency-track-results.json
                '''
            }
        }

        stage('Generate Report') {
            steps {
                // Usar Pandoc para generar un informe a partir del resultado de Dependency Track
                sh '''
                pandoc -s -o report.pdf <<EOF
                # Dependency Track Vulnerability Report

                ## Vulnerabilities
                $(cat dependency-track-results.json | jq -r '.vulnerabilities[] | "### \(.name)\nSeverity: \(.severity)\nDescription: \(.description)\nRecommendations: \(.recommendations)\n"')
                EOF
                '''
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

