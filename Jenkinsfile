pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker_connect')

	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t SuadaKoci/frontend:v1 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u suadakoci --password-976b831c-7951-4289-88e3-fae395de019e'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push SuadaKoci/frontend:v1'
			}
		}

		stage ('Kubernetis deploy'){
			steps {
					sh ("/usr/local/bin/kubectl -n testenv apply -f quiz-client.yml")
				
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
