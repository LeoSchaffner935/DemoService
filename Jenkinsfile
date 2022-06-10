node {
    def mvnHome = tool 'MyMaven'
    //def dockerImageTag = "leoschaffner935/dockerhub{env.BUILD_NUMBER}"

    stage('Clone Repo') {
        git 'https://github.com/LeoSchaffner935/DemoService.git'
    }

    stage('Build Project') {
        bat "mvn clean install -DskipTests"
    }

    stage('Build Image') {
        dockerImage = docker.build("leoschaffner935/dockerhub:latest") // :${env.BUILD_NUMBER}
    }

    stage('Deploy') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            //dockerImage.push("${env.BUILD_NUMBER}")
            dockerImage.push('latest')
        }
    }
}