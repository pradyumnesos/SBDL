pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               sh 'pipenv --python python3 sync'
            }
        }
        stage('Test') {
            steps {
               sh 'pipenv run pytest'
            }
        }
        stage('Package') {
	    when{
		    anyOf{ branch "master" ; branch 'release' }
	    }
            steps {
               sh 'zip -r sbdl.zip lib'
            }
        }
	stage('Release') {
	   when{
	      branch 'release'
	   }
           steps {
              echo 'you made a change in the release branch'
           }
        }
	stage('Deploy') {
	   when{
	      branch 'main'
	   }
           steps {
              echo 'you made a change in the deploy branch'
           }
        }
    }
}
