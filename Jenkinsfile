// Jenkinsfile
def setDetalleBuild(projectMetadata, imageEnv, branch) {
    def returnfuncion = [codResultado: "0", descResult: "", extResultFunction: ""]
    try {
        def jenkinsId = "#${currentBuild.number}"
        def version = projectMetadata.rootModule.moduleProps.version
        def entorno = imageEnv
        def tamanoRama = branch.size()
        def rama = (tamanoRama < 30) ? branch : "${branch.substring(0, 30)}..."
        
        currentBuild.displayName = "${jenkinsId} | ${version} | ${entorno} | ${rama}"
        println "Detalles del Pipeline: ${currentBuild.displayName}"
    } catch (Exception err) {
        returnfuncion.codResultado = "-1"
        returnfuncion.descResult = err.getMessage()
        println "Error al configurar detalles del Pipeline: ${err.getMessage()}"
        return returnfuncion
    }
    return returnfuncion
}

pipeline {
    agent any

    stages {
        stage('Ejecutar Pipeline') {
            steps {
                script {
                    def projectMetadata = [rootModule: [moduleProps: [version: '1.0.0']]]
                    def imageEnv = 'QA'
                    def branch = 'feature/nueva-funcionalidad'

                    def result = setDetalleBuild(projectMetadata, imageEnv, branch)

                    if (result.codResultado == "0") {
                        echo "Detalles del Pipeline configurados correctamente"
                    } else {
                        error "Error al configurar detalles del Pipeline: ${result.descResult}"
                    }
                }
            }
        }
    }

    post {
        always {
            // Puedes agregar pasos adicionales o notificaciones aquí
        }
    }
}
