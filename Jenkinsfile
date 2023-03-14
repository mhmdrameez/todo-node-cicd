pipeline {
    agent { label 'agent1' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/mhmdrameez/todo-node-cicd', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t mhmdrameez/node-todo-test:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push mhmdrameez/node-todo-test:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
