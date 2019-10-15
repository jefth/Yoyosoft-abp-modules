pipeline {
  agent any
  stages {
    stage('Build') {
      when {
        branch 'master'
      }
      steps {
        sh 'dotnet build'
        sh "echo ${env.NUGET_KEY}"
      }
    }
    stage('Releases') {
      when {
        branch 'master'
        expression {
          ciRelease action: 'check'
        }

      }
      steps {
        sh 'echo nuget上传'
        sh "echo ${env.NUGET_KEY}"
      }
    }
  }
  environment {
    NUGET_KEY = credentials('Yoyosoft-abp-modules-nuget-key')
    test = '123test'
  }
  triggers {
    githubPush()
  }
}