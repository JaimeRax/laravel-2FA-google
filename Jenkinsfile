pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/JaimeRax/laravel-2FA-google.git'
        PROJECT_DIR = 'laravel-2FA-google'
        PROJECT_ID = 'your_project_id'
        REPORT_FILE = 'report.pdf'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Verifica si el directorio del proyecto existe
                    if (!fileExists("${env.PROJECT_DIR}")) {
                        echo "El directorio ${env.PROJECT_DIR} no existe. Clonando el repositorio."
                        // Clona el repositorio si el directorio no existe
                        sh "git clone ${env.REPO_URL}"
                    } else {
                        echo "El directorio ${env.PROJECT_DIR} ya existe. Navegando al directorio."
                    }
                    // Navega al directorio del proyecto
                    dir("${env.PROJECT_DIR}") {
                        // Realiza un ls para listar el contenido del directorio
                        sh 'ls -la'
                    }
                }
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

