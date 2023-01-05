pipeline {
    agent any

    environment {
        registryCredential = 'DockerCredential'
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
                //checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mamun7025/spring-boot-tomcat-cicd.git']]])
                 echo 'Starting job, checkout'
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

        stage('S-4: Deploy to Tomcat') {
             steps {
               echo 'Start deploy...'
               deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://localhost:8082/')], contextPath: 'tm-app', war: '**/*.war'
            }
        }

        stage('S-5: Finished Job') {
           steps {
               echo 'Finished Job'
           }
        }

    }
    post {
        always {
            echo 'Finished CI/CD Job'
        }
    }

}