pipeline {
    // agent any
    agent { 
        docker { 
            image 'nginx'
            } 
        }
    stages{ 
        stage ("Dev"){
            steps {
                sh "nginx --version"
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