timestamps{
    node(){
        stage('Aqua Microscanner') {
            aquaMicroscanner imageName: 'mapit/mapit-dev', notCompliesCmd: 'exit 4', onDisallowed: 'fail', outputFormat: 'html'
         }
    }
}