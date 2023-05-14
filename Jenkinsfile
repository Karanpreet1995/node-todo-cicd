pipeline{
    agent { label 'Jenkins-Agent-1' }
    stages{
        stage('Code'){
            steps{
                git url:'https://github.com/Karanpreet1995/node-todo-cicd.git', branch: 'master'
                
            }
        }
        stage('Build and test'){
            steps{
               sh 'docker build . -t karanpreetkaurgill1995/node-todo-app:latest' 
            }
        }
        stage('Login and Push Image'){
            steps{
               echo 'Login into docker hub'
               withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPassword')]) {
                   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                   sh "docker push ${env.dockerHubUser}/node-todo-app:latest"
               }
            }
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
                
            }
        }
    }
}
