pipeline {
    agent {
        label 'ubuntu-agent'
    }

    options {
        skipDefaultCheckout()
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                deleteDir()

                git branch: 'master',
                    url: 'https://github.com/rabiacodes23/maven-cicd-project.git'
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
                archiveArtifacts(
                    artifacts: 'target/*.jar',
                    fingerprint: true
                )
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESSFUL!'
            echo 'Maven CI pipeline completed successfully.'
        }

        failure {
            echo 'BUILD FAILED! Check the console output.'
        }

        always {
            echo 'Pipeline execution completed.'
	    echo 'testing for jenkins trigger'
        }
    }
}
