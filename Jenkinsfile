pipeline {
  agent any
  stages {
    stage('update docker image') {
      steps {
        script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            withCredentials([usernamePassword(credentialsId: 'github_id', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')])  {
              sh "git config user.email yan.sovanseyha@gmail.com"
              sh "git config user.name sovanseyha"
              // sed : wanna change file 
              sh "sed -i \"s+sovanseyha/ui-fintrack.*+sovanseyha/ui-fintrack:${DOCKERTAG}+g\" dev/web-deployment.yaml"
              sh "git add ."
              sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
              sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/fintrack-cd.git HEAD:master"
            }
          }
        }
      }
    }
  }
}
