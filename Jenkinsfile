pipeline {
    agent any
       environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-diksha')
	}
       stages {
        stage('code') {
            steps {
               git 'https://github.com/sahu04/Assigment_Aaptatt.git'
            }
        }
        stage('build') {
            steps {
	       checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sahu04/Assigment_Aaptatt.git']])	    
               sh 'mvn package'
            }
       }
		stage('build docker image') {
			steps {
				sh 'docker build -t tomcat:latest .'
			}
		}
             stage('Login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				sh 'pwd'
			}
		}
              stage('Push') {
                        steps {
				sh 'docker tag tomcat dikshasahu/tomcat:latest'
				sh 'docker push dikshasahu/tomcat:latest'
			}
		}
       }
  }
