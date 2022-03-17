pipeline {
    
	  agent any
  tools {nodejs "node"}

	environment{
	registry="mrchelsea/testing-docker"
	registryCredential='dockerhub'
	dockerImage=''
	}
    
    //def registry = 'mrchelsea/testing-docker'
    //def registryCredential = 'dockerhub'
	stages{
	stage('Git') {
		steps{
		git 'https://github.com/rahulguptaft9/node-todo-frontend'
		}	
	}
	stage('Build') {
		steps{
		sh 'yarn install'
		}	
	}
	stage('Test') {
		steps{
		sh 'npm test'
		}
	}
	stage('Building image') {
		steps{
			script{
			 	dockerImage=docker.build registry	
			}
		}
	}
	stage('Registring image') {
		steps{
			script{
				docker.withRegistry('',registryCredential){
				dockerImage.push()
				}
			}
		}
	}
	}
    
}
