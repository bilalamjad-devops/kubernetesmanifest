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
                        
                        //👉 CHANGE: Set your own email and name for Git commits
                        sh "git config user.email Your-GitHub-email@example.com"
                        sh "git config user.name Your-GitHub-Name"
                        
                        // This updates the 'image' field in deployment.yaml to the new tag
                        //👉 CHANGE: Ensure the regex 'Your-Docker-Hub-Username/test.*' matches your YAML image string
                        sh "sed -i 's+Your-Docker-Hub-Username/test.*+Your-Docker-Hub-Username/test:${DOCKERTAG}+g' deployment.yaml"
                        
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        
                        // Ensure 'kubernetesmanifest.git' and the branch 'main' match your repo
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}

