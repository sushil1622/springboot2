pipeline {
    agent any
    
    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerblue')
	}
	
	stages {
	    
	    stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sushil1622/springboot270423.git']]])
            }
        }
        
	    stage('build') {
	        steps {
				sh 'sudo docker build -t erp:latest .'
			}
	    }
	    
	    stage('Push') {

			steps {
				sh 'docker push erp:latest'
			}
		}
		
		stage("kubernetes deployment"){
        sh 'kubectl apply -f eks-deploy-k8s.yaml'
    }
		
		
	}
	
}