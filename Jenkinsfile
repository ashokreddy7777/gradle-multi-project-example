pipeline {
    agent any 
    options{timeout (time: 1, unit:'HOURS')}

    stages{
        stage('Gradle Build'){
            sh '''
                gradle clean build
            '''    
        }

     stage('SonarQube analysis'){
       environment {
        scannerHome = tool 'sonarscanner'
       }
        steps{
         withSonarQubeEnv('sonar'){
         sh ''' 
            "${scannerHome}/bin/sonar-scanner" -Dsonar.java.binaries=. -Dsonar.projectKey=citrinesample -Dsonar.host.url=http://35.168.13.119:9000 -Dsonar.sourceEncoding=UTF-8
         '''     
        } 
      
      }
    }
}
}