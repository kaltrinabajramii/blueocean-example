node {
    def app
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        if (env.BRANCH_NAME == 'dev') {
            echo "Building image on 'dev' branch"
            app = docker.build("kaltrinabajramii/blueocean-example")
        } else {
            echo "Skipping build - Not on 'dev' branch"
        }
    }

    stage('Push image') {
        if (env.BRANCH_NAME == 'dev' && app) {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        } else {
            echo "Skipping push - Not on 'dev' branch"
        }
    }
}
