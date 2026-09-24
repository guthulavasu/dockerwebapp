
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
                echo 'SonarQube stage'
            }
        }
    }
}
