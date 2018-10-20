pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /home/vlad/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
	    	withMaven(
			// Maven installation declared in the Jenkins "Global Tool Configuration"
			maven: 'M3',
			mavenLocalRepo: '~/.m2/repository') {

		      // Run the maven build
		      sh "mvn -B -DskipTests clean package"

	    	}
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
				stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }				
    }
}

