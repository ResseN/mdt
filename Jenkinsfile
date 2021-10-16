pipeline{
    agent {
        label 'ubuntu_2004_agent'
    }
    stages{
        stage("Compressing"){
            parallel{
                stage("CleanCSS"){
                    steps{
                        nodejs(nodeJSInstallationName: 'NodeJS16'){
                            sh 'cleancss -O 2 -o www/min/*.css www/css/*.css'
                        }
                    }
                }
                stage("UglifyJS"){
                    steps{
                        nodejs(nodeJSInstallationName: 'NodeJS16'){
                            sh 'uglifyjs -o www/min/*.js www/js/*.js'
                        }
                    }
                }
            }
        }
    }
}
