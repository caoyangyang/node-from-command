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
            sh "docker build . -f docker/Dockerfile -t 'yangyangcao/node-from-command':${params.Version} --rm"
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
            sh "docker login --username= ${env.DockerHubUserName} --password=${env.DockerHubPassword}"
            sh "docker push yangyangcao/node-from-command:${params.Version}"
            sh "docker tag yangyangcao/node-from-command:${params.Version} yangyangcao/node-from-command:${env.GIT_VERSION}"
            sh "docker push yangyangcao/node-from-command:${env.GIT_VERSION}"
            sh "echo \"${env.GIT_VERSION}\""
          }
    }
  }
}