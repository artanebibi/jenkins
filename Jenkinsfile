node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    if (env.BRANCH_NAME == 'dev') {  // only dev branch
        stage('Build image') {
            app = docker.build("artanebibi/jenkins")
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        }
    } else {
        stage('Skip Docker Push') {
            echo "Skipping build & push because this is not 'dev'."
        }
    }
}
