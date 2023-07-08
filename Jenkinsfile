pipeline{
	agent any
	environment {
		DOCKERHUB_PASS = Yamini@2304
	}
	stages{
		stage("Building the Student Survey Image"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf surveyForm.war *'
					sh 'echo ${BUILD_TIMESTAMP}'
					sh 'docker login -u ygona -p ${DOCKERHUB_PASS}'
					sh 'docker build -t ygona/student-survey .'
				}
			}
		}
		stage("Pushing image to docker"){
			steps{
				script{
					sh 'docker push ygona/student-survey'
				}
			}
		}
		stage("Deploying to rancher"){
			steps{
				script{
					// sh 'kubectl set image deployment/survey container-0=krishna1303/survey -n 645clusternamespace'
					sh 'kubectl rollout restart deploy deployment -n swenamespace'
				}
			}
		}
	}
}
