pipeline {
    agent {
        label 'ubuntu-agent'
    }
     triggers {
        pollSCM('H/2 * * * *')
    }

    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Checkout') {
            steps {
                deleteDir()
                sh 'git clone --branch master https://github.com/rabiacodes23/maven-cicd-project.git .'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
	stage('Archive Artifact') {
	    steps {
        	archiveArtifacts artifacts: 'target/*.jar',
                        fingerprint: true
    	    }
	}
    }
    

    post {
        success {
            echo 'BUILD SUCCESSFUL!'
        }
        failure {
            echo 'BUILD FAILED! Check the console output.'
	    echo "testing webhook..."
	    echo "webhook successful"
        }
    }
}
