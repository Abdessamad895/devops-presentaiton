pipeline {
    agent any 
    
    tools{
        maven 'Maven'
    }
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/dorbanianas/devops-presentation.git'
            }
        }
        
        stage("Build"){
            steps {
                sh "mvn clean package"
            }
        }
        
        stage("Sonarqube Analysis "){
            steps{
                sh """
                    mvn sonar:sonar -Dsonar.url=http://localhost:9000/ -Dsonar.login=your_token -Dsonar.projectName=Devops \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=Devops
                """
            }
        }
        
        stage("Docker login"){
            steps {
                withCredentials([string(credentialsId: 'your_credentialID', variable: 'password')]) {
                    sh "docker login -u your_credentialID -p ${dockerhubpwd}"
                }
            }
        }
        
        stage("Docker push"){
            steps {
                 sh """ 
                        docker tag devopspresentation/devops-app:latest dockerpresentation/devops-app 
                        docker push dockerpresentation/devops-app
                    """ 
            }
        }
        
        stage("Docker run"){
            steps {
                 sh """
                        docker stop devops-app
                        docker rm devops-app
                        docker run --name devops-app -d -p 9090:8080 dockerpresentation/devops-app 
                    """ 
            }
        }
        
    }
}