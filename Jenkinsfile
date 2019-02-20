pipeline {
  agent {
    kubernetes {
      label 'mypodtemplate-v1'
      containerTemplate {
        name 'golang'
        image 'golang:1.10'
        ttyEnabled true
        command 'cat'
      }
      containerTemplate {
        name 'maven'
        image 'maven:3.6.0-jdk-8-alpine'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
      }
    }
    stage('Get a Maven project') {
      steps {
        git 'https://github.com/jenkinsci/kubernetes-plugin.git'
        container('maven') {
          sh 'mvn -B -X clean install'
        }
      }
    }
     stage('Get a Golang project') {
      steps {
        git 'https://github.com/hashicorp/terraform.git'
        container('golang') {
          sh '''
                    mkdir -p /go/src/github.com/hashicorp
                    ln -s `pwd` /go/src/github.com/hashicorp/terraform
                    cd /go/src/github.com/hashicorp/terraform && make core-dev
                    '''
        }
      }
    }
  }
}
