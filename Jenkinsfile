pipeline {
    agent any 
    options{timeout (time: 1, unit:'HOURS')}

    stages{
      stage('Gradle Build'){
          steps{
             
            sh '''
                gradle clean build
            '''    
        }
      }
     stage('SonarQube analysis'){
       environment {
        scannerHome = tool 'sonarscanner'
       }
        steps{
         withSonarQubeEnv('sonar'){
         sh ''' 
            "${scannerHome}/bin/sonar-scanner" -Dsonar.java.binaries=. -Dsonar.projectKey=test -Dsonar.sourceEncoding=UTF-8
         '''     
        } 
      
      }
    }
}
}
