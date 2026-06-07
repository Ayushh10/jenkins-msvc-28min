pipeline {
    // agent any
    agent { 
        docker { 
            image 'node'
            } 
        }
    stages{ 
        stage ("Dev"){
            steps {
                sh "node --version"
                echo "Dev Env"
            }
        }
        stage ("Stage"){
            steps {
                echo "Stage Env"
            }
        }
        stage ("Prod"){
            steps {
                echo "Prod Env"
            }
        }
    }
}