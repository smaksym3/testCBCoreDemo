pipeline {
  agent {
    kubernetes {
      label 'mypodtemplate-v1'
      containerTemplate {
        name 'golang'
        image 'golang:1.8.0'
        ttyEnabled true
        command 'cat'
      }
      containerTemplate {
        name 'maven33'
        image 'maven:3.3.9-jdk-8-alpine'
        ttyEnabled true
        command 'cat'
      }
      containerTemplate {
        name 'maven36'
        image 'maven:3.6.0-jdk-12-alpine'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run maven 3.3') {
      steps {
        container('maven33') {
          sh 'mvn -version'
        }
      }
    }
    stage('Get a Maven project') {
      steps {
        git 'https://github.com/jenkinsci/kubernetes-plugin.git'
        container('maven36') {
          sh 'mvn -B -X clean install'
        }
      }
    }
  }
}
