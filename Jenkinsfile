pipeline {
    agent any
    
    stages{
        stage ("Clone"){
            steps{
                echo "Clone The Code"
                git url: "https://github.com/VenkateshVunnam/django-notes-app.git", branch:"main"
            }
        }
        stage ("Build"){
            steps{
                echo "Building the Code"
                sh "docker build -t my-notes-app ."
            }
            
        }
        stage ("Push to Docker Hub"){
            steps{
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker tag my-notes-app ${env.dockerhubUser}/my-notes-app:v1"
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker push ${env.dockerhubUser}/my-notes-app:v1"
                }
            }
        }
        stage ("Deploy"){
            steps{
                echo "Deploying the Container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }   
           
}
     
    
