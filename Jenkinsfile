pipeline {
  agent any
  stages {
     stage("test"){
      steps{
          bat './gradlew test'
          archiveArtifacts 'build/test-results/test/'
          cucumber buildStatus: 'UNSTABLE',
                          reportTitle: 'My report',
                          fileIncludePattern: '*/.json',
                          trendsLimit: 10,
                          classifications: [
                              [
                                  'key': 'Browser',
                                  'value': 'Firefox'
                              ]
                          ]
      }
    }
 stage("Code Analysis"){
    steps{

      withSonarQubeEnv('sonar') {
                        bat "./gradlew sonar"
                    }
    }
    }
 stage("Code Quality") {
             steps {
                 waitForQualityGate abortPipeline: true
             }
         }

stage("Build") {
          steps {
              bat './gradlew build'
              bat './gradlew javadoc'
              archiveArtifacts 'build/libs/*.jar'
              archiveArtifacts 'build/docs/'
          }
      }


 stage("Deploy & notification"){
            steps {
                bat './gradlew publish'
            }
            post {
                  success {
                       notifyEvents message: 'Success ',
                       token: '1_xdr6m1f2hyoyro1ymngz57xjpjsu4d'
                       mail to: 'km_mohandouali@esi.dz',
                       subject: "Success",
                       body: "Deployment successful"
                  }
                  failure {
                        notifyEvents message: 'Failure',
                        token: '1_xdr6m1f2hyoyro1ymngz57xjpjsu4d'
                        mail to: 'km_mohandouali@esi.dz',
                        subject: "Failure",
                        body: "Something went wrong "


                  }
            }
        }







}
}