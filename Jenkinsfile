// Job 2: CD Pipeline (Manifest Update)

node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    // 'github' must match your Jenkins Credentials ID for Git
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        
                        //👉 CHANGE: Set your own email and name for Git commits - Your-GitHub-email@example.com, Your-GitHub-Name
                        sh "git config user.email devopsengineerbilalamjad@gmail.com"
                        sh "git config Bilal Amjad "
                        
                        // This updates the 'image' field in deployment.yaml to the new tag
                        //👉 CHANGE: Ensure the regex 'Your-Docker-Hub-Username/test.*' matches your YAML image string
                        sh "sed -i 's+bilalamjaddevops/test.*+bilalamjaddevops/test:${DOCKERTAG}+g' deployment.yaml"
                        
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        
                        // Ensure 'kubernetesmanifest.git' and the branch 'main' match your repo
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}

