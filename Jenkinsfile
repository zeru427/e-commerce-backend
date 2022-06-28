node {
    def mvnHome = tool 'MyMaven'
    def dockerImageTag = "zeruyang001/zerudockerhub{env.BUILD_NUMBER}"
    stage('clone repo'){
        git 'https://github.com/zeru427/project2.git'
        mvnHome = tool 'MyMaven'
    }
    stage('Build Project 2'){
        //sh    linux
        bat "C:\\Maven\\apache-maven-3.8.5\\bin\\mvn clean install"
        //jar file will be generated
    }
    stage('Build docker image'){
        dockerImage = docker.build("zeruyang001/zerudockerhub:${env.BUILD_NUMBER}")
    }
    stage('Build docker deploy'){
        echo "Docker Image Tag name : ${dockerImageTag}"
        //docker-hub-credentials - we have to create in jenkins credentials
        docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials') {
            dockerImage.push("e-commerce-backend-${env.BUILD_NUMBER}")
            dockerImage.push("e-commerce-backend-project2-latest")
        }
    }
}
