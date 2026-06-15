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

        // Define your Docker Hub username and image name
        REGISTRY_CREDS = 'dockerhub' // This matches the Jenkins Credential ID
        IMAGE_NAME     = 'killwishh/currency-exchange-devops'
        IMAGE_TAG      = "${BUILD_TAG}"
        
    }
    stages{ 
        stage ("Dev"){
            steps {
                echo "Dev Env"
                sh "mvn --version"
                sh "docker --version"

                echo "Build"
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD ID - $env.BUILD_ID"
                echo "Job Name - $env.JOB_NAME"
            }
        }
        stage ("Compile"){
            steps {
                sh "mvn clean compile"
            }
        }
        stage ("package"){
            steps {
                sh "mvn package -DskipTests"
            }
        }
        // stage ("Test"){
        //     steps {
        //         sh "mvn test"
        //     }
        // }
        // stage ("Integration Test"){
        //     steps {
        //         sh "mvn failsafe:integration-test failsafe:verify"
        //     }
        // }

        stage ("Build Docker Image"){
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                sh 'docker login -u $USER -p $PASS'
                script {
                // Default
                // docker build -t killwishh/currency-exchange-devops:${env.BUILD_TAG}
                docker Image = docker.build("killwishh/currency-exchange-devops:${env.BUILD_TAG}")
                    }
                }
            }
        }
        stage ("Push Docker Image") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) 
                sh 'docker login -u $USER -p $PASS'
                script {
                    docker.withRegistry('https://docker.io', "${REGISTRY_CREDS}") {
                        dockerImage.Push();
                        dockerImage.Push("latest");
                    }
                }
            }
        }
    }
}