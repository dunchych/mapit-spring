pipeline{  
    agent {
        docker { image 'ibmcase/docker:18.09-dind' }
    }
    stages{
        stage('Checkout') {
            steps{
                git branch: 'master', url: 'https://github.com/dunchych/mapit-spring.git'

            }
        }

    stage('Build') {
        steps{
            sh 'mvn clean package -DskipTests'
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

