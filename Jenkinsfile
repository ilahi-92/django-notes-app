pipeline {
    agent any
    
    stages{
        stage("Clone Code"){
            steps {
                echo "cloning the code"
                git url:"https://github.com/ilahi-92/django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps {
                echo " building the image"
                sh "docker build -t notes-app ."
            }
        }
        stage("push to docker hub"){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag notes-app ${env.dockerHubUser}/notes-app:latest"    
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
        stage("deploy"){
            steps {
                echo "deploying the application on to container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}





