node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        when {
            branch 'dev' // Only run this stage for the 'dev' branch
        }
        steps {
            app = docker.build("bmilenkov/kiii-jenkins")
        }
    }
    stage('Push image') {
        when {
            branch 'dev' // Only run this stage for the 'dev' branch
        }
        steps {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    }
}
