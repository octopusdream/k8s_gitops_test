node {
    def app
    env.JENKINS_IP = 'jenkins-1d89f623e089d4f6.elb.ap-northeast-3.amazonaws.com'
    stage('Clone repository') {    
        checkout scm
    }
    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email yusine51@gmail.com"
                    sh "git config user.name YUYUYUJINN"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+${JENKINS_IP}:5001/flask_test.*+${JENKINS_IP}:5001/flask_test:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/octopusdream/k8s_gitops_test.git HEAD:master"
                }
            }
        }
    }
}
