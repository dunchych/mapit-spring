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



    stage('Scan') {
        steps{
            aquaMicroscanner imageName: 'mapit/mapit-dev', notCompliesCmd: 'exit 4', onDisallowed: 'fail', outputFormat: 'html'
         }
    }
}
}

