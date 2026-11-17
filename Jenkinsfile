pipeline {
    agent any
    
    stages {
        
        stage ('Identify Branch') {
            steps {
                echo "current branch: ${env.BRANCH_NAME}"
            }
        }
        stage('Checkout') {
            steps {
                echo 'Source code checkout completed'
                sh 'git log -1 --oneline'
            }
        }
        stage('Build') {
            steps{
                echo "Building java app"
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Running unit tests'
                sh 'mvn test'
            }
        }
	stage ('Package'){
            steps {
                sh 'mvn package'
            }
        }

        stage('main branch validation') {
            when {
                branch 'main'
            }
            steps {
                echo "executing main branch validation"
            }
        }
        stage ('develop branch validation') {
            when {
                branch 'develop'
            }
            steps {
                echo "executing develop branch validation"
            }
        }
        stage ('Feature branch validation') {
            when {
                expression {
                    env.BRANCH_NAME.startsWith('feature/')
                }
            }
            steps {
                echo "executing feature branch validation"
            }
        }
    }
}
