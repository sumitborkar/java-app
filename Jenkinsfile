pipeline {
  agent any
  environment{
    VERSION="${env.BUILD_ID}"
  }
  stages{
    // stage("Sonar quality check"){
    //    agent {
    //       docker{
    //         image 'openjdk:11'
    //       }
    //    }
    //    steps{
    //      script{
    //        withSonarQubeEnv(credentialsId: 'sonar-token1', installationName: 'sonarserver') {
    //           sh 'chmod +x ./gradlew'
    //           sh './gradlew sonarqube'
    //        }
    //        timeout(time: 1, unit: 'HOURS') {
    //                  def qg = waitForQualityGate()
    //                  if (qg.status != 'OK') {
    //                       error "Pipeline aborted due to quality gate failure: ${qg.status}"
    //                  }
    //                }
    //      }
    //    }
    // }
    stage("Docker build and Docker push"){
      steps{
        script{
          withCredentials([string(credentialsId: 'docker_pass_nexus', variable: 'docker_pass')]) {
            sh '''
            docker build -t 192.168.163.139:8082/springapp:${VERSION} .
            docker login -u admin -p $docker_pass 192.168.163.139:8082
            docker push 192.168.163.139:8082/springapp:${VERSION}
            docker rmi 192.168.163.139:8082/springapp:${VERSION}
            '''
          }

        }
      }

    }
  }
}
