pipeline {
    agent {
        node {
            label 'docker-node'
        }
    }

    tools {
        maven 'mymaven'
    }

    stages {

        stage('Git') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
                sh 'cp -r target Docker-app/'
            }
        }

        stage('SonarQube') {
            steps {
                withSonarQubeEnv('mysonar') {
                    sh '''
                        mvn verify \
                        org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                        -Dsonar.projectKey=myproject
                    '''
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t appimage Docker-app'
                sh 'docker build -t dbimage Docker-db'
            }
        }
        stage('trivy-stage') {
            steps {
                sh 'trivy image appimage'
                sh 'trivy image dbimage'
            }
        }
    }
}
