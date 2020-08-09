pipeline {
	agent any
	stages {

		stage('Create Kubernetes Cluster') {
			steps {
				withAWS(region:'us-east-1', credentials:'aws_credentials') {
					sh '''
						eksctl create cluster \
						--name OCSCluster \
						--version 1.17 \
						--region us-east-1 \
						--nodegroup-name standard-workers \
						--node-type t3.medium \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
					'''
				}
			}
		}

		stage('Configure kubectl') {
			steps {
				withAWS(region:'us-east-1', credentials:'aws_credentials') {
					sh '''
						aws --region us-east-1 eks update-kubeconfig --name OCSCluster
					'''
				}
			}
		}

	}
}
