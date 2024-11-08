node {
    def app

    stage('Clone repository') {
        /* Clone the repository to the Jenkins workspace */
        checkout scm
    }

    stage('Build image') {
        /* Build the Docker image */
        app = docker.build("bayoojo1/devops-prj-1")
    }

    stage('Test image') {
        /* Run a simple test inside the Docker container */
        app.inside("-v ${pwd()}:/workspace") {
            // Use the mounted directory for running commands inside the container
            sh 'cd /workspace && echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Push the Docker image to the registry with build number and 'latest' tags */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
