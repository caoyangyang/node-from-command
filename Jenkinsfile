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
    stage('Push to Repo') {
          environment {
            GIT_VERSION = sh (
              script:"git rev-parse HEAD",
              returnStdout: true
            ).trim()
          }
          steps {
            sh "git rev-parse HEAD"
            sh "docker push tw/node-form-command:${params.Version}"
            sh "docker tag tw/node-form-command:${params.Version} tw/node-form-command:${env.GIT_VERSION}"
            sh "docker push tw/node-form-command:${env.GIT_VERSION}"
            sh "echo \"${env.GIT_VERSION}\"
          }
    }
  }
}