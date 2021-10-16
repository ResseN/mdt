pipeline{
    agent {
        label 'ubuntu_2004_agent'
    }
    stages{
        stage("Compressing"){
            parallel{
                stage("JS"){
                    steps{
                        nodejs(nodeJSInstallationName: 'NodeJS16'){
                            sh 'find www/js/ -name "*.js" -printf \'%f\n\'| xargs -I {} uglifyjs www/js/{} -o www/min/min.{}'
                        }
                    }
                }
                stage("CSS"){
                    steps{
                        nodejs(nodeJSInstallationName: 'NodeJS16'){
                            sh 'find www/css/ -name "*.css" -printf \'%f\n\'| xargs -I {} cleancss www/css/{} -o www/min/min.{}'
                        }
                    }
                }
            }
        }
        stage("Archieving"){
            steps{
                sh 'tar cf mdt.tar --exclude=.git* --exclude=www/css --exclude=www/js --exclude=mdt.tar . '
            } 
        }
    }
}
