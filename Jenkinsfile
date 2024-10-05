pipeline{
    agent any
    tools{
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages{
        stage('Clone'){
            steps{
                git url:'https://github.com/ArchitAvd/config-confer',branch:'master'
            }
        }
        stage('Build'){
            steps{
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test'){
            steps{
                bat "mvn test"
            }
        }
        stage('Deploy'){
            steps{
                bat "docker rm -f my-conf-container"
                bat "docker rmi -f my-conf-image"
                bat "docker build -t my-conf-image ."
                bat "docker run -p 8088:8088 -d --name my-conf-container my-conf-image"
            }
        }
    }
}