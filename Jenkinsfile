#!groovy

pipeline {
  agent any
  stages {
 /*
     stage("Git Clone"){
       steps{
     //   git credentialsId: '', url: 'https://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@github.com/stefanmucha/spring-petclinic'
       }
    }
*/
     stage(' Build') {
      steps{
        
           sh './gradlew clean build -x test'
        }
    }

    
    stage('Pre deply clean') {
      agent any
      steps {
    //    sh './gradlew build'
       
        //sh 'docker stop muchast2/spring-petclinic:latest'
        //sh 'docker images --quiet | xargs docker stop'
        //sh 'docker images --quiet --filter=dangling=true | xargs --no-run-if-empty docker rmi -f'
        //sh 'docker images --quiet | xargs --no-run-if-empty docker rmi -f'
        //sh 'docker container prune -f'
        sh 'docker container stop $(docker container ls -aq)'
        sh 'docker container rm $(docker container ls -aq)'
        sh 'docker image prune -f'
      }
    }
    
    
    stage('Docker Build') {
      agent any
      steps {

        sh 'docker build --no-cache -t muchast2/spring-petclinic:latest .'
       }
    }
    
    stage('Docker run') {
      agent any
      steps {
      sh 'docker run -p 8081:8080 muchast2/spring-petclinic:latest &'
   
      }
    }
    
}
}
