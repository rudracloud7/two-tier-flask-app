@Library("Shared") _
pipeline{
    
    agent { label "dev"};
    
    stages{
        stage("Code"){
            steps{
                scripts{
                     git url: "https://github.com/rudracloud7/two-tier-flask-app.git", branch: "master"
                }
            }    
        }
        stage("Trivy file System"){
            steps{
                scripts{
                    trivy_fs()
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
                scripts{
                    docker_push("dockerHubCreds","two-tier-flask")
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
