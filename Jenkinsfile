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








}
}