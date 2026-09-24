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
    }
}
