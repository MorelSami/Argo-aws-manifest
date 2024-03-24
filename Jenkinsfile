node {
    def app
    
    env.IMAGE = 'smorel237/amazon'

    stage('Access argo manifest repository') {
             git branch: 'main', 
             url: 'https://github.com/MorelSami/Argo-aws-manifest.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'smorel-github-2024', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        //script  {def IMAGE='easnae817/amazon'}
                        sh "git config user.email mksami237@gmail.com"
                        sh "git config user.name Morel Sami"
                        //sh "git switch master"
                        sh "cat deployment.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Argo-aws-manifest.git HEAD:main"
             }
         }
     }
  }
}
