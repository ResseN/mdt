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
                            sh 'find www/js/ -name "*.js" -print | xargs uglifyjs {} -o www/min/minimized.{}'
                        }
                    }
                }
                stage("CSS"){
                    steps{
                        nodejs(nodeJSInstallationName: 'NodeJS16'){
                            sh 'cleancss --batch --batch-suffix \'.mini\' www/css/*.css  -o www/min/*.'
                        }
                    }
                }
            }
        }
    }
}
