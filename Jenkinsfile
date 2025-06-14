pipeline {
    agent {
        label 'windows'
    }

    environment {
        DEP_CHECK_PATH = 'C:\\Herramientas\\dependency-check\\bin\\dependency-check.bat'
    }

    stages {
        stage('Instalar dependencias') {
            steps {
                bat 'npm install'
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                bat 'npm test'
            }
        }

        stage('Análisis con Dependency-Check') {
            steps {
                bat "${DEP_CHECK_PATH} --project \"SafeNotes\" --scan . --format HTML --out dependency-check-report"
            }
        }

        stage('Publicar reporte') {
            steps {
                archiveArtifacts artifacts: 'dependency-check-report/dependency-check-report.html', fingerprint: true
            }
        }
    }
}
