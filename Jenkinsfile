pipeline {

    agent any
    //agent {
      //  node {
        //  label 'agent1'
        //}
      //}

    // using the Timestamper plugin we can add timestamps to the console log
    options {
        timestamps()
    }

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Checkout') {
            steps {
                sh '''
                    echo "Checking Out"
                '''
                checkout scm
                stash 'everything'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                    mvn clean install -DskipTests
                '''
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging....'
                sh '''
                    mvn package -DskipTests
                '''
            }
        }
        stage('Publish') {
            steps {
                echo 'Deploying....'
                sh '''
                    mvn deploy -DskipTests
                '''
            }
        }
        stage('End') {
            steps {
                echo 'Build is finished..'
            }
        }
    }
}
