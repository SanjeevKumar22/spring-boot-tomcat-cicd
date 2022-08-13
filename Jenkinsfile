pipeline {
    agent any

    environment {
        imageName = 'mn7025/spring-boot-docker-cicd-v2'
        containerName = 'spring-boot-docker-cicd-v2'
        registryCredential = 'DockerCredential'
        dockerImage = ''
    }

    triggers {
        pollSCM('* * * * *') //polling for changes, here once a minute
    }

    stages {
        stage('S-1: Starting Job') {
            steps {
                echo 'Starting job, cleaning workspace'
                deleteDir()
            }
        }
        stage('S-2: Checkout code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mamun7025/spring-boot-tomcat-cicd.git']]])
            }
        }
        stage('S-3: Gradle build') {
            steps {
                bat 'gradlew.bat clean build'
            }
        }
        stage('S-3: Test') {
             steps {
                echo 'Starting test'
            }

        }

        stage('S-4: Building docker image') {
            steps{
                echo 'Start deploy...'
            }
        }

        stage('S-5: Push image to dockerhub') {
        	steps{
        		echo 'Start deploy...'
        	}
        }


        stage('S-6: Deploy') {
             steps {
               echo 'Start deploy...'
            }
        }


        stage('S-9: Run Docker container on remote hosts') {
            steps {
                echo 'Run Docker container on remote hosts'
                // sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 4001:80 nikhilnidhi/nginxtest"
            }
        }


    }
    post {
        always {
            echo 'Finished CI/CD Job'
        }
    }
}