pipeline {
    agent any 
    options{timeout (time: 1, unit:'HOURS')}

    stages{
      stage('Gradle Build'){
          environment {
          gradleHome = tool 'gradle'
       }
          steps{
             
            sh '''
                "${gradleHome}/bin/gradle" clean build
            '''    
        }
      }
     stage('SonarQube analysis'){
       environment {
        scannerHome = tool 'sonar-scanner'
       }
        steps{
         withSonarQubeEnv('sonar'){
         sh ''' 
            "${scannerHome}/bin/sonar-scanner" -Dsonar.java.binaries=. -Dsonar.projectKey=test -Dsonar.sourceEncoding=UTF-8 -Dsonar.sources=.
         '''     
        } 
      
      }
    }
     stage('ws cleanup'){
      steps{
        cleanWs()
      }
    }   
}
}
