#!/usr/bin/env groovy

cleanWs()
node('master') {
  stage('checkout') {
    checkout(
      [
        $class: 'GitSCM',
        branches: [
          [
            name: '*/master'
          ]
        ],
        extensions: [],
        userRemoteConfigs: [
          [
            url: 'https://github.com/DwivedyGyan/the-example-app.nodejs.git'
          ]
        ]
      ]
    )
  }
  stage('NPM: Installing dependencies') {
    sh 'npm install'
  }
  stage('CODE QUALITY: ESLint') {
    sh 'npm run lint'
  }
  stage('CODE DUPLICASY: jscpd') {
    sh 'npm run cpd'
  }
  stage('BUG Scanning: OWASP Dependency-Check') {
    sh 'npm run owasp'
  }
}
