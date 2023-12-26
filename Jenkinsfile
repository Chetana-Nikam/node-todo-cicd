pipeline {
    agent { label "dev-agent"}
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/Chetana-Nikam/node-todo-cicd.git", branch: "master"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage("build and test"){
            steps{
                sh "sudo docker build -t node-app-test-new ."
                echo 'code build bhi ho gaya'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "sudo docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                sh "sudo docker push ${env.dockerHubUser}/node-app-test-new:latest"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "sudo docker-compose down && sudo docker-compose up -d"
                echo 'deployment ho gayi'
            }
        }
    }
}
