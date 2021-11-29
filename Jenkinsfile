pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhublogin')

	}
    
	stages {

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username=suadakoci --password=Jennastojku12'
			}
		}
        stage('Build') {

			steps {
				sh 'docker build -t suadakoci/angular-frontend:v1 .'
			}
		}


		stage('Push') {

			steps {
				sh 'docker push suadakoci/angular-frontend:v1'
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
