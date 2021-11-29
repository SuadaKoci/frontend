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

		stage ('Kubernetes deploy'){
			steps {
        sh ("kubectl apply -f quiz-client.yml | -k /usr/local/bin/kubectl")
				
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
