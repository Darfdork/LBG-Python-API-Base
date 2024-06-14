pipeline {
    agent any
    environment{
        DOCKER_IMAGE="lbg"
        PORT =5001
    }
    stages {
        stage('BuildCleanup') {
            steps {
                sh "echo 'Cleaning up system'"
                sh "sleep 3"
                sh "docker rm -f \$(docker ps -aq) || true"
                sh "docker rmi -f \$(docker images)|| true"
                sh "echo 'Clean up Complete' "
                }
        }
        stage('Build the container'){
            steps{
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('Modify the application') {
            steps {
                sh "echo 'Modify application'"
                sh "sleep 3"
                sh "export PORT=5001"
                sh "echo 'Modifications Done. Port is now set to ${PORT}'"
                }
        }
        stage('Deploy Containers'){
            steps{
                sh "echo 'Running Docker Container...'"
                sh "sleep 3"
                sh "docker run -d -p 80:${PORT} -e PORT=${PORT} ${DOCKER_IMAGE}"
            }
            }
        }
}    

