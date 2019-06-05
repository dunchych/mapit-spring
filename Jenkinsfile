pipeline{  
    agent any
    stages{
        stage('Checkout') {
            steps{
                git branch: 'master', url: 'https://github.com/dunchych/mapit-spring.git'

            }
        }

    stage('Build') {
        steps{
            sh 'mvn clean package'
         }
    }

    stage('Package') {
        steps{
            docker.build("mapit/mapit-dev")
         }
    }

    stage('Scan') {
        steps{
            aquaMicroscanner imageName: 'mapit/mapit-dev', notCompliesCmd: 'exit 4', onDisallowed: 'fail', outputFormat: 'html'
         }
    }
}
}