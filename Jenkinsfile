pipeline { 
    agent any 
    environment { 
        NODE_VERSION = '18.16'
    } 
 
    stages { 
        stage('Clonar Repositorio') {
            steps {
                git 'https://github.com/DamarisRamirez/desafio_jenkins.git'
            }

        }
 
        stage('Dependencias') { 
            steps { 
                script { 
                    try { 
                        echo "⚙️ Instalando dependencias..." 
                        bat 'npm install' 
                    } catch (Exception e) { 
                        error("❌ Error en la etapa de dependencias") 
                    } 
                } 
            } 
        } 
 
        stage('Test') { 
            steps { 
                script { 
                    try { 
                        echo "🧪 Ejecutando pruebas..." 
                        bat 'npm test' 
                    } catch (Exception e) { 
                        error("❌ Error en la etapa de Test") 
                    } 
                } 
            } 
        } 

        stage('Docker') {
            steps {
                script {
                    def imagen = 'desafio_jenkins:latest'
                    bat "docker build -t ${imagen} ."
                }
            }
        } 
    } 
 
    post { 
        success { 
            echo "✅ Pipeline completado con éxito" 
        } 
        failure { 
            echo "❌ El pipeline ha fallado" 
        } 
    } 
}