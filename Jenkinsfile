pipeline {
  agent {
    kubernetes {
      label 'mypodtemplate-v1'
      containerTemplate {
        name: 'golang'
        image: 'golang:1.8.0'
        ttyEnabled: true
        command: 'cat'
      }
      containerTemplate {
        name 'maven'
        image 'maven:3.3.9-jdk-8-alpine'
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
          sh 'mvn -B clean install'
        }
      }
    }
  }
}
