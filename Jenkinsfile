pipeline{
    
    agent { label "dev"};
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/rudracloud7/two-tier-flask-app.git" , branch: "master"
            }    
        }
        stage("Trivy file System"){
            steps{
                sh "trivy fs . -o reuslts.json
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("Test"){
            steps{
                echo "Developer likh ke dega"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser",
                )]){
                    
                sh "docker login -u $dockerHubUser -p $dockerHubPass"
                sh "docker image tag two-tier-flask-app $dockerHubUser/two-tier-flask-app"
                sh "docker push $dockerHubUser/two-tier-flask-app:latest"
            
                }    
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
     }
  }
