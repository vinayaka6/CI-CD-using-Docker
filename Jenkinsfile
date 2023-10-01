pipeline
{
    agent any
    tools {
       maven 'maven project'
    }
    stages 
    {
        stage ('git  checkout') 
        {
            steps
            {
                git 'https://github.com/vinayaka6/maven_test.git'
            }
        }
        stage ('execute maven')
        {
            steps
            {
            sh 'mvn package'
        
            }
        }
        stage ('docker remove existing container')
        {
            steps
            {
                sh 'docker stop kcontainer'
                sh 'docker rm kcontainer'
            }
        }



        stage ('docker build and run')
        {
            steps
            {
                sh 'docker build -t kwebapp:latest .'
                sh 'docker run -itd --name kcontainer -p 8123:8080 kwebapp'
            }
        }
        stage ('docker Tag and push')
        {
            steps 
            {
                sh 'docker tag kwebapp:latest vinayaka8/ubuntu'
                withDockerRegistry(credentialsId: 'dockerhub', url: 'https://hub.docker.com/repository/docker') {
                // some block
                }
                sh 'docker push vinayaka8/ubuntu'
            }
            
        }
        stage('Run Docker container on remote hosts') 
        {
             
            steps 
            {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
            }
        }

    }
}

        
