pipeline{
    agent any


    tools {
        maven 'M2_HOME'
    }


	stages {


 stage('Getting project from Git') {
            steps{
      			checkout([$class: 'GitSCM', branches: [[name: '*/main']],
			extensions: [],
			userRemoteConfigs: [[url: 'https://github.com/nedrioussama/devopsfront-oussema.git']]])
            }
        }


        stage('Cleaning the project') {
            steps{
                sh "npm install"
            }
        }





        stage('Artifact Construction') {
            steps{
                sh "ng build  "
            }
        }



stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t oussamanedri/angular-app:latest .'
                          }
                      }
                  }




                  stage('login dockerhub') {
                                        steps {
                                      sh 'docker login -u oussamanedri -p oussDockerhub99'
                                            }
		  }





	                      stage('Push Docker Image') {
                                        steps {
                                   sh 'docker push oussamanedri/angular-app:latest'
                                            }
		  }



        stage('Run Angular Container') {
                      steps {
                          script {
                            sh 'docker-compose up -d'
                          }
                      }
                  }

}


}
