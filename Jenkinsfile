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
                sh 'composer install'
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
                sh 'dependency-track --project d11f0baf-29b4-4035-9110-b484c2018f5f --api-key odt_YMvH1o1YLuHFLBPovCCd22eli4QqcONb --file dependency-track-results.json'
            }
        }

        stage('Generate Report') {
            steps {
                // Generar el archivo Markdown con los resultados del análisis
                sh '''
                #!/bin/bash
                echo "# Dependency Track Vulnerability Report" > report.md
                echo "" >> report.md
                echo "## Vulnerabilities" >> report.md
                jq -r '.vulnerabilities[] | "### \(.name)\nSeverity: \(.severity)\nDescription: \(.description)\nRecommendations: \(.recommendations)\n"' dependency-track-results.json >> report.md

                # Convertir Markdown a PDF usando Pandoc
                pandoc report.md -o report.pdf
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
