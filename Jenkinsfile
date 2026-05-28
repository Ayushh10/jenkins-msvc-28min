pipeline {
    // agent any
    agent { docker { image 'maven'} }
    stages{ 
        stage ("Dev"){
            steps {
                sh 'mvn --version'
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