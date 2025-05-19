pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
               git branch: 'main', url: 'https://github.com/AyushKole/ashokit_ecomm_store.git'
            }
        }
        
        stage('Docker Image'){
            steps{
                sh 'docker build -t ayushkole45/ecomm_store .'
            }
        }
        
       stage('Docker Image push'){
            steps{
            withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {
                   sh 'docker login -u ayushkole45 -p ${docker_pwd}'
                   sh 'docker push ayushkole45/ecomm_store'
            }
            }
        }
        
         stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }  
        
        
    }
}
