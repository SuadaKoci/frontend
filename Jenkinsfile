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
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $suadakoci --password-Jennastojku12'
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
