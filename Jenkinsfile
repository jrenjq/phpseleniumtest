pipeline {
	agent none
	stages {
		// stage('Integration UI Test') {
		// 	parallel {
				stage('Deploy') {
					agent any
					steps {
						sh 'docker run -d -p 80:80 --name my-apache-php-app -v c:\\Users\\jren\\Documents\\GitHub\\jenkins-php-selenium-test\\src:/var/www/html php:7.2-apache'
						input message: 'Finished using the web site? (Click "Proceed" to continue)'
						sh 'docker stop my-apache-php-app'
					}
				}
				stage('Headless Browser Test') {
					agent {
						docker {
							image 'maven:3-alpine' 
							args '-v /root/.m2:/root/.m2' 
						}
					}
					steps {
						sh 'mvn -B -DskipTests clean package'
						sh 'mvn test'
					}
					post {
						always {
							junit 'target/surefire-reports/*.xml'
						}
					}
				}
		// 	}
		// }
	}
}