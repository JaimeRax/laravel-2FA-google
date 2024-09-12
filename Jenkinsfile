pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/JaimeRax/laravel-2FA-google.git'
        PROJECT_DIR = 'laravel-2FA-google'
        PROJECT_ID = '5d86a645-d745-48ba-8103-844839eec0e9'
        REPORT_FILE = 'report.pdf'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo 'hola mundo'
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
    }

    post {
        always {
            // Limpia los archivos temporales si es necesario
            cleanWs()
        }
    }
}

