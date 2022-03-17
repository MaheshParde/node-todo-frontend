pipeline {
    
	  agent any
  tools {nodejs "node"}

	environment{
	registry="maheshparde/rect-test"
	registryCredential='dockerhub'
	dockerImage=''
	}
    
    //def registry = 'mrchelsea/testing-docker'
    //def registryCredential = 'dockerhub'
	stages{
	stage('Git') {
		steps{
		git 'https://github.com/MaheshParde/node-todo-frontend'
		}	
	}
	stage('Build') {
		steps{
		sh 'yarn'
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
