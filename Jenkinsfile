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
                            sh 'uglifyjs www/js/*.js -o www/min/*.minimized.js'
                        }
                    }
                }
                stage("CSS"){
                    steps{
                        nodejs(nodeJSInstallationName: 'NodeJS16'){
                            sh 'cleancss -O2 www/css/*.css -o www/min/*.minimized.css'
                        }
                    }
                }
            }
        }
    }
}
