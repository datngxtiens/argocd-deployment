pipeline {
    agent any
    stages {       
        stage('Update deployment') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                        withCredentials([usernamePassword(credentialsId: 'datngxtiens-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]){
                            sh "git config user.email datngxtiens@gmail.com"
                            sh "git config user.name 'datngxtiens'"
                            sh "cat deployment.yaml"
                            sh "sed -i 's+datngxtiens/gitops-demo.*+datngxtiens/gitops-demo:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done get update manifest version: ${env.BUILD_NUMBER}'"
                            // sh "echo ${GIT_PASSWORD}"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-deployment.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
