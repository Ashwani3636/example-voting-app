pipeline{
    agent{
        label "worker"
    }
    stages{
        stage("docker build and push"){
            steps{
                sh '''
                    cd vote
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 128308815363.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t 128308815363.dkr.ecr.us-east-1.amazonaws.com/application:latest-${BUILD_NUMBER} .
                    docker push 128308815363.dkr.ecr.us-east-1.amazonaws.com/application:latest-${BUILD_NUMBER}
                    sh "docker stop $(docker ps -a -q)"
                    sh "docker run -itd -p 81:80 128308815363.dkr.ecr.us-east-1.amazonaws.com/application:latest-${BUILD_NUMBER}"

                    '''
            }
        }
    }
}
