pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
               git 'https://github.com/openwriteup/java11-jenkins.git'
            }
        }
	  stage('build') {
            steps {
               sh '''sudo docker build -t softechie/myjava1:latest -f dockerfile .
'''
            }
        }
		  stage('token') {
            steps {
               sh ''' echo "place token here" |docker login -u softechie --password-stdin
'''
            }
        }
		 stage('push') {
            steps { 
               sh ''' sudo docker push softechie/myjava1:latest
'''
            }
        }

    }
}
