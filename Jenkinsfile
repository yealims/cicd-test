pipeline {
	agent any

	stage{
	  stage('Github Pull') {
	    steps {
	        git branch: 'main',url:'https://github.com/yealims/cicd-test.git'
	    }
	  }
	  stage('Git clond end') {
	    steps {
	        sh 'touch cicd_test.txt'
	        sh 'echo "git clone end" > cicd_test.txt'
	    }
	  }
}