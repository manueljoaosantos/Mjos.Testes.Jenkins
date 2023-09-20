pipeline{

  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }

	stages {

		stage('Test') {

			steps {				
				sh 'docker info'
			}
		}

		stage('Build') {

			steps {				
				sh 'docker build -t Mjos.Testes.Jenkins/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Tag') {

			steps {
				sh 'docker tag Mjos.Testes.Jenkins/nodeapp_test:latest mjsantos/teste'
			}
		}
		
		stage('Push') {

			steps {
				sh 'docker push mjsantos/teste'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
