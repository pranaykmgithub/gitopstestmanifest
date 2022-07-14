node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        bat "git config user.email m.pranay31@gmail.com"
                        bat "git config user.name pranaykmgithub"
                        //sh "git switch master"
                        bat "cat deployment.yaml"
                        bat "sed -i 's+pranaykmdocker/test.*+pranaykmdocker/test:${DOCKERTAG}+g' deployment.yaml"
                        bat "cat deployment.yaml"
                        bat "git add ."
                        bat "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        bat "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
