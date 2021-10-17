node ("ubuntu_2004_agent") {
    stage("Compressing"){
        compressing = ["JS" :nodejs('NodeJS16'){sh 'find www/js/ -name "*.js" -printf \'%f\n\'| xargs -I {} uglifyjs www/js/{} -o www/min/min.{}'},
                      "CSS" :nodejs('NodeJS16'){sh 'find www/css/ -name "*.css" -printf \'%f\n\'| xargs -I {} cleancss www/css/{} -o www/min/min.{}'}]
    parallel compressing
    }
    stage("Archieving") {
        sh 'tar cf mdt.tar --exclude=.git* --exclude=www/css --exclude=www/js --exclude=mdt.tar . '
        archiveArtifacts artifacts: 'mdt.tar', allowEmptyArchive: false, fingerprint: true, onlyIfSuccessful: true
    }
    stage("Publication") {
        def server = Artifactory.server 'Artifactory_week_ass'
        def uploadSpec = '''{
                "files": [
                    {
                    "pattern": "mdt.tar",
                    "target": "general-repo-local/${BRANCH_NAME}/mdt.v.${BUILD_NUMBER}.tar"
                    }
                ]
            }'''
        server.upload spec: uploadSpec
    }
}
