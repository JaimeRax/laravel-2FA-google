pipeline {
    agent any

    environment {
        // Variables de entorno que puedes configurar en Jenkins
        REPO_URL = 'https://github.com/JaimeRax/laravel-2FA-google.git'
        PROJECT_ID = '5d86a645-d745-48ba-8103-844839eec0e9'
        REPORT_FILE = 'report.pdf'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clona el código fuente desde el repositorio Git usando la variable de entorno REPO_URL
                git url: "${env.REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                // Instala dependencias PHP usando Composer
                sh 'cd laravel-2FA-google'
                //sh 'composer install'
                sh 'ls'
            }
        }

        //stage('Build') {
        //    steps {
        //        // Ejecuta el build si es necesario para Laravel
        //        // Por ejemplo, si tienes scripts específicos para construir el proyecto
        //        sh 'php artisan migrate' // Asegúrate de que esto sea necesario para tu build
        //    }
        //}
        //
        //stage('Dependency Track Analysis') {
        //    steps {
        //        // Ejecuta el análisis de dependencias con Dependency-Track usando la variable de entorno PROJECT_ID
        //        sh "dependency-track-cli --analyze --project ${env.PROJECT_ID}"
        //    }
        //}
        //
        //stage('Generate Report') {
        //    steps {
        //        // Genera un informe con Pandoc a partir de los resultados del análisis
        //        // Asumiendo que los resultados se guardan en results.json
        //        sh "pandoc results.json -o ${env.REPORT_FILE}"
        //    }
        //}
        //
        //stage('Archive Report') {
        //    steps {
        //        // Archiva el informe generado como un artefacto del build
        //        archiveArtifacts "${env.REPORT_FILE}"
        //    }
        //}
    }

    post {
        always {
            // Limpia los archivos temporales si es necesario
            cleanWs()
        }
    }
}

