pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checkout completed'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t devops-cicd-app:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Test') {
            steps {
                sh 'docker run --rm devops-cicd-app:${BUILD_NUMBER}'
            }
        }

        stage('Ansible Deploy') {
	    steps {
       		 sh 'ansible-playbook deploy.yml --extra-vars "build_number=${BUILD_NUMBER}"'
      	   }
       }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed. Check the console output.'
        }
    }
}
