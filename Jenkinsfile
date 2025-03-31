node {
    def app
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        if (env.BRANCH_NAME == 'dev') {  // Only build on dev branch
            app = docker.build("bmilenkov/kiii-jenkins")
        }
    }

    stage('Push image') {
        if (env.BRANCH_NAME == 'dev') {  // Only push from dev branch
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        }
    }
}
