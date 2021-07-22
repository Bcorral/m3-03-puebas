pipeline {
    agent any
    tools {
        maven "maven3.8.1"
        jdk "jdk16"
    }
    stages {
        stage("Env Variables") {
            steps {
                sh "printenv"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Sonar'){
        	steps{
        	sh 'mvn verify sonar:sonar -Dsonar.projectKey=Bcorral_m3-03-puebas -Dsonar.organization=bcorral -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=462188e22cd55e26eb5df4aca84bddadbeb20192 -Dsonar.branch.name=master'
        	
        	}
        	
        }
    }
}