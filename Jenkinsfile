pipeline{  
    agent any
    stages{
        stage('Checkout') {
            steps{
                git branch: 'microscanner-jenkinsci', url: 'https://gitlab.com/aboullaite/Jib-Springboot.git'

            }
        }

    stage('Build') {
        steps{
            sh 'mvn clean package -DskipTests'
         }
    }

    stage('Package') {
        steps{
            docker.build("aboullaite/sb-app")
         }
    }

    stage('Scan') {
        steps{
            aquaMicroscanner imageName: 'aboullaite/sb-app', notCompliesCmd: 'exit 4', onDisallowed: 'fail', outputFormat: 'html'
         }
    }
}
}