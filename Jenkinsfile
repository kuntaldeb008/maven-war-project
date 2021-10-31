pipeline{
    agent any
    
    environment {
     DOCKER_TAG = getVersion()
    }
    
    stages{
        stage('SCM'){
            steps{
                git branch: 'main',
                credentialsId: 'github',
                url: 'https://github.com/kuntaldeb008/maven-war-project.git'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        
        stage('Docker Build'){
            steps{
                sh "docker build . -t kuntaldeb008/javaapp:${DOCKER_TAG} "
            }
        }
        
        stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                  sh "docker login -u kuntaldeb008 -p ${dockerHubPwd}"
                }
                
                sh "docker push kuntaldeb008/javaapp:${DOCKER_TAG} "
            }
        }
        
        stage('Docker Deploy'){
            steps{
              ansiblePlaybook credentialsId: 'dev-server', disableHostKeyChecking: true, extras: "-e DOCKER_TAG=${DOCKER_TAG}", installation: 'ansible', inventory: 'dev.inv', playbook: 'deploy-docker.yml'
            }
        }
    }    
}

def getVersion(){
   def commitHash = sh returnStdout: true, script: 'git rev-parse --short HEAD'
   return commitHash
}
