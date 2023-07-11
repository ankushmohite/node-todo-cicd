pipeline {
    agent { label 'dev' }

    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/ankushmohite/node-todo-cicd.git', branch: 'master'
            }
           
        }
        
        stage('Build and test'){
            steps {
                sh 'docker build . -t ankushmohite/node-todo-cicd:latest'
            }
           
        }
        
        stage('Login and push Image'){
            steps{
                echo 'Logging in to docker hub and pushing iamge...'
                withCredentials([usernamePassword(credentialsID:'dockerhub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push ankushmohite/node-todo-cicd:latest"
                }
            }
        }
             
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
           
        }
    }
}
