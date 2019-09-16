pipeline {
  agent any
  parameters {
      string(
        name: 'Version',
        defaultValue:"latest",
        description: "Docker version in hub")
  }

  tools {nodejs "node"}

  stages {

    stage('Cloning Git') {
      steps {
        git 'https://github.com/caoyangyang/node-from-command.git'
      }
    }

    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
         sh 'npm test'
      }
    }
    stage('Build Docker Image') {
          steps {
            sh "docker build . -f docker/Dockerfile -t 'tw/node-form-command':${params.Version} --rm"
          }
        }

  }
}