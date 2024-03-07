pipeline{
    agent any

    stages{
        stage('sonar quality check'){
            agent{
                docker{
                    image 'maven'
                    args '-u root'
                }
            }
            steps{
                
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                       sh "mvn sonar:sonar" 
                    }
                }
            }
        }
        stage('Quality Gate status'){
          steps{
            scripts{
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
            }
          } 
        }
    }
}