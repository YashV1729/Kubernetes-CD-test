node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email yash.raj@gmail.com"
                        sh "git config user.name YashV1729"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+yashrv1729/public.*+yashrv1729/public:${DOCKERTAG}+g' deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Commit Jenkins Job change manifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Kubernetes-CD-test.git HEAD:main"
      }
    }
  }
}
}
