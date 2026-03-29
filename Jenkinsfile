pipeline {
    agent any 
    stages {
        stage ("code clon") {
            steps {
                git url : "https://github.com/Rahul10052023/two-tier-flask-app.git", branch : "master"   
                echo " Code clone Successfully"
            }
        }
        stage ("build and push in docker hub") {
            steps {
                withCredentials([ usernamePassword(
                    credentialsId:"dockerhubcred",
                    passwordVariable:"dockerhubPass",
                    usernameVariable:"dockerhubUser"
                )] ){
                sh " docker build -t my-jenkins-test-app ."
                sh " docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass} "
                sh " docker tag my-jenkins-test-app ${env.dockerhubUser}/my-jenkins-test-app:v2"
                sh "docker push ${env.dockerhubUser}/my-jenkins-test-app:v2"
            }
         }
    }
        stage (" Docker compose up ") {
            steps {
                sh " docker compose up -d "
            }
        }
        
        stage ("test") {
            steps {
                echo "This is test stage"
                
            }
        }
        stage ("deploy") {
            steps {
                echo "This is deploy stage"
            }
            
        }
        stage("debug") {
            steps {
                sh 'pwd'
                sh 'ls -l'
                
            }
            }
        
    }
    
}
            
