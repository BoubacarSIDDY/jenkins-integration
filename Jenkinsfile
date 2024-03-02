pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                 bat "E:/cours/M1/JAVA/apache-maven-3.8.6/bin/mvn clean package"
            }
        }
        stage('Test') {
            steps {
                 bat "E:/cours/M1/JAVA/apache-maven-3.8.6/bin/mvn test"
            }
        }
         stage('Deploy') {
            steps {
                 bat 'docker build -t boubacarsiddy/jenkins-integration .'
            }
        }
         stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub_credentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    bat "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                    bat "docker tag jenkins-integration:1.0 boubacarsiddy/jenkins-integration"
                    bat "docker push boubacarsiddy/jenkins-integration:1.0"
               }
            }
       }
    }
}
