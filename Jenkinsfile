pipeline {
    agent any
    // agent { 
    //     docker { 
    //         image 'node'
    //         } 
    //     }

    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages{ 
        stage ("Dev"){
            steps {
                echo "Dev Env"
                sh "maven --version"
                sh "docker version"

                echo "Build"
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD ID - $env.BUILD_ID"
                echo "Job Name - $env.JOB_NAME"
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