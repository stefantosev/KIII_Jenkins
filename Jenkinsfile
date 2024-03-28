 node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("walkorion/kiii-jenkins")
    }
    stage('Push image') {   
        withDockerRegistry([credentialsId: 'dockerhub', url: 'https://registry.hub.docker.com']) {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }