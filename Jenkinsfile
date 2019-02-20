def label = "mypod-${UUID.randomUUID().toString()}"
podTemplate(label: label, containers: [
    containerTemplate(name: 'maven36', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'maven33', image: 'maven:3.3.9-onbuild-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'golang', image: 'golang:1.10', ttyEnabled: true, command: 'cat')
  ]) {

    node(label) {
        
        stage('Build a Maven project 33') {
            git 'https://github.com/jenkinsci/kubernetes-plugin.git'
            container('maven33') {
                stage('Build a Maven project') {
                    sh '''
                        env
                        mvn -version
                       '''
                }
            }
        }
        
        stage('Build a Maven project 36') {
            git 'https://github.com/jenkinsci/kubernetes-plugin.git'
            container('maven36') {
                stage('Build a Maven project') {
                    sh '''
                       env
                       mvn -version
                       #mvn -B clean install
                       '''
                }
            }
        }

        stage('Build a Golang project') {
            git url: 'https://github.com/hashicorp/terraform.git'
            container('golang') {
                stage('Build a Go project') {
                    sh '''
                    env
                    #mkdir -p /go/src/github.com/hashicorp
                    #ln -s `pwd` /go/src/github.com/hashicorp/terraform
                    #cd /go/src/github.com/hashicorp/terraform && make tools
                    '''
                }
            }
        }

    }
}
