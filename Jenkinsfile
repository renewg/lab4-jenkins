pipeline {
    agent any

    options {
        disableConcurrentBuilds() // Deshabilitamos build concurrentes
        timestamps()                  // Añadimos marcas te tiempo
        timeout(5)                  // Establecemos un timeout de 5 min.
    }

    // Creación de variables de entorno
    environment {
        FORCE_COLOR = "0"
        NO_COLOR = "true"
    }

    // Declaración de etapas
    stages {
        // Apartado 3
        stage('Audit tools') {
            steps {
                sh 'node --version'
            }
        }

        // Etapa 4: Instalar las dependencias
        stage('Install dependecies') {
            steps {
                sh 'npm install'
            }
        }

        // Etapa 5: Creación de ficheros autogenerados
        stage('Generate files') {
            steps {
                sh 'npm run prisma:generate'
            }
        }

        // Etapa 6: Chequeo del formato de código
        stage('Format Check') {
            steps {
                sh 'npm run format:check'
            }
        }

        // Etapa 7: Chequeo de calidad del código
        stage('Code quality') {
            steps {
                sh 'npm run lint'
            }
        }

        // Etapa 8: Chequeo de tipos
        stage('Type check') {
            steps {
                sh 'npm run type-check'
            }
        }

        // Etapa 9: Ejecución de tests
        stage('Tests') {
            steps {
                sh 'npm run test'
            }
        }

        // Etapa 10: Construcción y archivado
        stage('Build') {
            steps {
                sh 'npm run build'
                archiveArtifacts artifacts: 'dist/', fingerprint: true, followSymlinks: false
            }
        }
    }
    // Etapas finales.
    post {
        always { // Siempre que se finalice
            cleanWs()
        }
        success { // Cuando finalice correctamente
            echo 'Pipeline completed successfully!'
        }
        failure { // Cuando finalice con error
            echo 'Pipeline failed. Review logs.'
            
        }
    }

}