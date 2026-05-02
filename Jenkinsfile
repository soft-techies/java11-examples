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
               sh '''sudo docker build -t softechie/myjava:latest -f dockerfile .
'''
            }
        }
		  stage('token') {
            steps {
               sh ''' echo "dckr_pat_ZZ0evWF_3zrpi3THpIrTb1-ATzg" |docker login -u softechie --password-stdin
'''
            }
        }
		 stage('push') {
            steps { 
               sh ''' sudo docker push softechie/myjava:latest
'''
            }
        }

    }
}
