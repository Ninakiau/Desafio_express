pipeline { 
    agent any 
    environment { 
        NODE_VERSION = '18.16'
    } 
 
    stages { 
        stage('Clonar Repositorio') {
            steps {
                echo "*" "Clonando el repositorio..."
                git 'https://github.com/Ninakiau/Desafio_express.git'
                checkout scm
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
                    bat "docker build -t desafio_jenkins ."
                    bat "docker run -p 3000:3000 desafio_jenkins"
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